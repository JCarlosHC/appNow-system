<template>
<ul class="list-group">
    <li class="list-group-item">
        Income total (100 %)
        <span class="badge">
          <price :value="Total"></price>
        </span>
    </li>
    <li class="list-group-item">
        Income AppNow (30%)
        <span class="badge">
          <price :value="Company"></price>
        </span>
    </li>
    <li class="list-group-item">
        Income teachers (70%)
        <span class="badge">
          <price :value="Instructors"></price>
        </span>
    </li>
</ul>
</template>

<script>
import price from './global.price.vue'
export default {
  name: 'widgetincome',
  components: { price },
  props: {
    month: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      Total: 0,
      Company: 0,
      Instructors: 0
    }
  },
  mounted() {
    this.get();
  },
  methods: {
    get() {
      let self = this;
      $.post('/panel/WidgetGetIncomes', {
        month: self.month
      }, function(r) {
        self.Total = r.Total;
        self.Company = r.Company;
        self.Instructors = r.Instructors;
      }, 'json')
    }
  }
}
</script>