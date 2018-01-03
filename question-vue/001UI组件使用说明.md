## UI组件使用说明
##### css组件需要引入并且注册后才能使用，js组件只需引入而无需注册即可使用
> 例： 在这里Button是css组件，Toast, Indicator是js组件，不用注册是需要使用
```
<script>
  import { Button, Toast, Indicator } from 'mint-ui'
  export default {
    methods: {
      toast1: function () {
        Toast('toast1')
      }，
      indicator1: function () {
        Indicator.open()
      }
    },
    components: {
      'mt-button': Button
    }
  }
</script>
```
