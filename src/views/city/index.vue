<template>
  <div class="city-select">
    <el-select v-model="province" filterable placeholder="请选择省份/市">
      <el-option
        v-for="item in options"
        :key="item.name"
        :label="item.name"
        :value="item.name"
      />
    </el-select>
    <el-select v-model="cityLevel" filterable placeholder="请选择城市">
      <el-option
        v-for="item in cityLevelarr"
        :key="item.name"
        :label="item.name"
        :value="item.name"
      />
    </el-select>
    <el-select v-model="district" filterable placeholder="请选择区县">
      <el-option
        v-for="item in districtarr"
        :key="item"
        :label="item"
        :value="item"
      />
    </el-select>
  </div>
</template>
<script>

import { getCity } from '@/api/city'
console.log(getCity)
export default {
  name: 'CITY',
  data() {
    return {
      options: getCity,
      cityLevelarr: '',
      districtarr: '',
      province: '',
      cityLevel: '',
      district: ''
    }
  },
  watch: {
    province: function() {
      this.updateCity()
      this.updatedistrict()
    },
    cityLevel: function() {
      this.updatedistrict()
    }
  },
  methods: {
    updateCity: function() {
      for (const i in this.options) {
        const obj = this.options[i]
        if (obj.name === this.province) {
          this.cityLevelarr = obj.city
          break
        }
      }
      this.cityLevel = this.cityLevelarr[0].name
    },
    updatedistrict: function() {
      for (const i in this.cityLevelarr) {
        const obj = this.cityLevelarr[i]
        if (obj.name === this.cityLevel) {
          this.districtarr = obj.area
          break
        }
      }
      if (this.districtarr.length > 0) this.district = this.districtarr[0]
    }
  }
}

</script>
