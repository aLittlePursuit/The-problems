# axios
> 在vue中定义成公共js文件来调用（例http.js）

```
import axios from 'axios'
import qs from 'qs'
axios.defaults.transformRequest = [data => qs.stringify(data)]
axios.defaults.baseURL = 'http://192.168.2.132/api/'

function checkStatus (response) {
  if (response && (response.status === 200 || response.status === 304 || response.status === 400)) {
    return response.data || response
  }
  return {
    status: -404,
    msg: '网络异常'
  }
}

function checkCode (res) {
  if (res.status === 404) {
    alert(res.msg)
  }
  return res.data || res
}

export default {
  get (url, params) {
    return axios.get(url, {params: params})
      .then(
        (response) => {
          return checkStatus(response)
        }
      ).catch(
        (error) => {
          return checkCode(JSON.parse(JSON.stringify(error)).response)
        }
      )
  },
  post (url, data) {
    return axios.post(url, data)
      .then(
        (response) => {
          return checkStatus(response)
        }
      ).catch(
        (error) => {
          return checkCode(JSON.parse(JSON.stringify(error)).response)
        }
      )
  }
}
```
> 调用方法（另创建js文件来调用这个js方法）（例：getData.js）

```
import http from './文件路径/http'

/**
 * 直播首页列表接口数据请求
 * */
export const live = () => http.get('/live_all', {})

/**
 * 直播分类列表接口数据请求
 * @param param   {String}  分别是'all','coming','review','onlive','subscribe'
 * @param openId  {String}  登陆后个人的open_id，为了测试这里传值为定值
 */
export const liveList = (param, openId) => http.get('/live_list', {
  type: param,
  open_id: openId
})

/**
 * 直播详情接口数据获取
 * @param id  {String}  每个直播单元所对应的id,通过这个请求道对应的数据来完成渲染
 */
export const liveDetail = (id, openId) => http.get('/live_detail', {
  room_id: id,
  open_id: openId
})

/**
 * 直播详情收藏（取消收藏）接口数据获取
 * @param id  {String}  直播间id
 * @param op  {String}  操作收藏（add）取消收藏（remove）
 * @param openId  {String}  用户id
 */
export const liveCollection = (id, op, openId) => http.post('/live_collection', {
  live_id: id,
  action: op,
  open_id: openId
})

/**
 * 直播详情关注（取消关注）接口数据获取
 * @param id  {String}  主播id
 * @param op  {String}  操作关注（add）取消关注（remove）
 * @param openId  {String}  用户id
 */
export const liveAttention = (id, op, openId) => http.post('/live_attention', {
  follow_who: id,
  action: op,
  open_id: openId
})

/**
 * 有密码房间接口数据请求
 * @param id  {String} 该房间id
 * @param pw  {String} 输入房间的密码
 */
export const lockRoom = (id, pw) => http.post('/live_pwd', {
  room_id: id,
  roompwd: pw
})

/**
 * 获取科室分类接口数据请求
 */
export const liveCategory = () => http.get('/live_category', {})

/**
 * 直播间申请接口数据请求
 */
export const liveApply = (categoryId, apTitle, apDetail, apNotice, apStartTime, apEndTime, logoSrc, roomSet, roomPwd, managerId, blacklistId, openId) => http.post('/live_apply', {
  category_id: categoryId,
  title: apTitle,
  detail: apDetail,
  notice: apNotice,
  launch_time: apStartTime,
  end_time: apEndTime,
  logo: logoSrc,
  room_set: roomSet,
  room_pwd: roomPwd,
  manager_id: managerId,
  blacklist_id: blacklistId,
  open_id: openId
})

/**
 * 直播申请图片上传接口
 */
export const liveApplyUploadPic = (base64) => http.post('/live_upload_pic', {
  data: base64
})
```
> 项目中的调用方式

```
import { live } from './文件路径/getData'

export default {
    name: 'live',
    mounted () {
      this.requesLive()   // 页面加载完成调取方法
    },
    methods: {
      // 直播首页列表接口数据请求
      async requesLive () {
        const list = await live()
        tconsole.log(list)
      }
    }
  }
```
