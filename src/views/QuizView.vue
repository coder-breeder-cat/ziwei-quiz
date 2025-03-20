<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref, reactive } from 'vue'
import { useForm } from 'vee-validate'
import * as yup from 'yup'

const schema = yup.object({
  habit: yup.number().required('請選擇是否有算命的習慣'),
  meOther: yup.string().default('other').required('請輸入其他'),
  knowledge: yup.string().required('請選擇對紫微斗數的了解程度'),
  interest: yup.string().required('請選擇是否對紫微斗數有興趣'),
  functionV: yup.number().required('請選擇希望程式具備的功能'),
  usage: yup.string().required('請選擇使用頻率'),
  preference: yup.string().required('請選擇喜歡的介面風格'),
  prOther: yup.string().default('other').required('請輸入其他'),
  payment: yup.string().required('請選擇付費方式'),
  acHabit: yup.string().required('請選擇是否有記帳的習慣'),
  fortune: yup.string().required('請選擇是否喜歡貼身助理'),
  informV: yup.number().required('請選擇想知道的生活資訊'),
  age: yup.string().required('請選擇年齡層'),
  gender: yup.string().required('請選擇性別'),
  industry: yup.string().required('請選擇職業類別')
})

const { defineField, handleSubmit, errors } = useForm({
  validationSchema: schema
})

const [habit] = defineField('habit')
const channel = ref('')
const method = ref('')
const [meOther] = defineField('meOther')
const [knowledge] = defineField('knowledge')
const [interest] = defineField('interest')
const functions = reactive({
    analysis: false,
    reminder: false,
    suggestion: false,
    knowledge: false
});
const [functionV] = defineField('functionV')
const [usage] = defineField('usage')
const [preference] = defineField('preference')
const [prOther] = defineField('prOther')
const [payment] = defineField('payment')
const [acHabit] = defineField('acHabit')
const frequency = ref('')
const [fortune] = defineField('fortune')
const inform = reactive({
    work: false,
    finance: false,
    love: false,
    family: false
})
const [informV] = defineField('informV')
const [age] = defineField('age')
const [gender] = defineField('gender')
const [industry] = defineField('industry')
const position = ref('')

const onChangeMethods = (e) => {
    if (e.target.value == '4') meOther.value = ''
    else meOther.value = 'other'
}

const onChangePreference = (e) => {
    if (e.target.value == '3') prOther.value = ''
    else prOther.value = 'other'
}

const onChangeFunctions = (e) => {
    if (!functionV.value) functionV.value = 0
    if (e.target.checked) functionV.value += 1
    else functionV.value -= 1
    if (functionV.value <= 0) functionV.value = null
}

const onChangeInform = (e) => {
    if (!informV.value) informV.value = 0
    if (e.target.checked) informV.value += 1
    else informV.value -= 1
    if (informV.value <= 0) informV.value = null
}

const onSubmit = handleSubmit((values) => {
  console.log('表單提交成功：', values)
  // 這裡可以添加提交表單的邏輯
})
</script>

<template lang="pug">
form(@submit.prevent="onSubmit")
    h1 完成問卷，獲得專屬你的紫微斗數簡易命盤！
    div 參與我們的問卷，了解更多關於紫微斗數的神秘世界，並獲得專屬於你的簡易命盤！

    ol
        li
            h3 請問您平常有算命的習慣嗎？*
            input(type="radio" value="0" v-model="habit") 
            span 從來沒有
            input(type="radio" value="1" v-model="habit") 
            span 偶爾會
            input(type="radio" value="2" v-model="habit") 
            span 經常算
            span.error(v-if="errors.habit") {{ errors.habit }}

        li
            h3 請問您通常透過什麼方式算命？
            input(type="radio" value="0" v-model="channel")
            span 親自去找老師
            input(type="radio" value="1" v-model="channel")
            span 上網找免費算命
            input(type="radio" value="2" v-model="channel")
            span 上網付費算命

        li
            h3 請問您平常喜歡用什麼方式算命？
            input(type="radio" value="0" v-model="method" @change="onChangeMethods")
            span 紫微斗數
            input(type="radio" value="1" v-model="method" @change="onChangeMethods")
            span 星座星盤
            input(type="radio" value="2" v-model="method" @change="onChangeMethods")
            span 八字卜卦
            input(type="radio" value="3" v-model="method" @change="onChangeMethods")
            span 塔羅牌
            input(type="radio" value="4" v-model="method" @change="onChangeMethods")
            span 其他
            input(v-if="method == '4'" type="text" placeholder="請輸入其他" v-model="meOther")
            span.error(v-if="errors.meOther") {{ errors.meOther }}

        li
            h3 你知道紫微斗數是什麼嗎？*
            input(type="radio" value="0" v-model="knowledge")
            span 完全不知道
            input(type="radio" value="1" v-model="knowledge")
            span 聽過但不熟
            input(type="radio" value="2" v-model="knowledge")
            span 知道一些
            input(type="radio" value="3" v-model="knowledge")
            span 很了解
            span.error(v-if="errors.knowledge") {{ errors.knowledge }}

        li
            h3 你對紫微斗數有興趣嗎？*
            input(type="radio" value="0" v-model="interest")
            span 當然有興趣
            input(type="radio" value="1" v-model="interest")
            span 沒什麼興趣
            span.error(v-if="errors.interest") {{ errors.interest }}

        li
            h3 請問您希望程式具備哪些功能？*
            input(type="checkbox" value="0" v-model="functions.analysis" @change="onChangeFunctions")
            span 命盤分析
            input(type="checkbox" value="1" v-model="functions.reminder" @change="onChangeFunctions")
            span 每日運勢提醒
            input(type="checkbox" value="2" v-model="functions.suggestion" @change="onChangeFunctions")
            span 感情、事業、財運建議
            input(type="checkbox" value="3" v-model="functions.knowledge" @change="onChangeFunctions")
            span 命理知識分享
            span.error(v-if="errors.functionV") {{ errors.functionV }}

        li
            h3 請問您平常使用程式的頻率是？*
            input(type="radio" value="0" v-model="usage")
            span 每天都用
            input(type="radio" value="1" v-model="usage")
            span 每週用幾次
            input(type="radio" value="2" v-model="usage")
            span 每月用幾次
            input(type="radio" value="3" v-model="usage")
            span 需要時才用
            span.error(v-if="errors.usage") {{ errors.usage }}

        li
            h3 請問您喜歡什麼樣的程式介面風格？*
            input(type="radio" value="0" v-model="preference" @change="onChangePreference")
            span 簡潔易懂
            input(type="radio" value="1" v-model="preference" @change="onChangePreference")
            span 專業詳細
            input(type="radio" value="2" v-model="preference" @change="onChangePreference")
            span 視覺化圖表
            input(type="radio" value="3" v-model="preference" @change="onChangePreference")
            span 其他
            input(v-if="preference == '3'" type="text" placeholder="請輸入其他" v-model="prOther")
            span.error(v-if="errors.preference") {{ errors.preference }}
            span.error(v-if="errors.prOther") {{ errors.prOther }}

        li
            h3 請問您平常會怎麼選擇付費方式？*
            input(type="radio" name="payment" value="0" v-model="payment")
            span 免費使用
            input(type="radio" name="payment" value="1" v-model="payment")
            span 付費訂閱
            input(type="radio" name="payment" value="2" v-model="payment")
            span 單次付費
            span.error(v-if="errors.payment") {{ errors.payment }}

        li
            h3 請問您平常有記帳的習慣嗎？*
            input(type="radio" value="0" v-model="acHabit") 
            span 從來沒有
            input(type="radio" value="1" v-model="acHabit") 
            span 偶爾會
            input(type="radio" value="2" v-model="acHabit") 
            span 經常算
            span.error(v-if="errors.acHabit") {{ errors.acHabit }}

        li
            h3 您通常多久記一次帳？
            input(type="radio" value="0" v-model="frequency") 
            span 從來不記
            input(type="radio" value="1" v-model="frequency") 
            span 一個月記一次
            input(type="radio" value="2" v-model="frequency") 
            span 每週記一次
            input(type="radio" value="3" v-model="frequency") 
            span 每天都記

        li
            h3 如果有一個貼身助理每天告訴你運勢變化，你會覺得怎麼樣？*
            input(type="radio" value="0" v-model="fortune")
            span 很喜歡
            input(type="radio" value="1" v-model="fortune")
            span 不喜歡
            span.error(v-if="errors.fortune") {{ errors.fortune }}

        li
            h3 每天想知道哪些類型的生活資訊呢？*
            input(type="checkbox" v-model="inform.work" @change="onChangeInform")
            span 工作
            input(type="checkbox" v-model="inform.finance" @change="onChangeInform")
            span 財務
            input(type="checkbox" v-model="inform.love" @change="onChangeInform")
            span 感情
            input(type="checkbox" v-model="inform.family" @change="onChangeInform")
            span 家庭
            span.error(v-if="errors.informV") {{ errors.informV }}
            

    h1 個人基本資料

    ol
        li
            h3 請問您的年齡層為？*
            input(type="radio" value="0" v-model="age")
            span 20 歲以下
            input(type="radio" value="1" v-model="age")
            span 21 - 30 歲
            input(type="radio" value="2" v-model="age")
            span 31 - 40 歲
            input(type="radio" value="3" v-model="age")
            span 41 - 50 歲
            input(type="radio" value="4" v-model="age")
            span 51 - 60 歲
            input(type="radio" value="5" v-model="age")
            span 超過60歲
            span.error(v-if="errors.age") {{ errors.age }}

        li
            h3 請問您的生理性別為？*
            input(type="radio" value="0" v-model="gender")
            span 男
            input(type="radio" value="1" v-model="gender")
            span 女
            span.error(v-if="errors.gender") {{ errors.gender }}
        li
            h3 請問您的目前職業類別為？*
            input(type="radio" name="industry" value="0" v-model="industry")
            span 科技業   
            input(type="radio" name="industry" value="1" v-model="industry")
            span 金融業
            input(type="radio" name="industry" value="2" v-model="industry")
            span 製造業
            input(type="radio" name="industry" value="3" v-model="industry")
            span 服務業
            input(type="radio" name="industry" value="4" v-model="industry")
            span 醫療業
            input(type="radio" name="industry" value="5" v-model="industry")
            span 教育業
            input(type="radio" name="industry" value="6" v-model="industry")
            span 營造業
            input(type="radio" name="industry" value="7" v-model="industry")
            span 餐飲業
            span.error(v-if="errors.industry") {{ errors.industry }}

        li
            h3 請問您目前的職位是？
            input(type="radio" value="0" v-model="position")
            span 管理職
            input(type="radio" value="1" v-model="position")
            span 行銷職
            input(type="radio" value="2" v-model="position")
            span 研發職
            input(type="radio" value="3" v-model="position")
            span 業務職
            input(type="radio" value="4" v-model="position")
            span 行政職
            input(type="radio" value="5" v-model="position")
            span 客服職
            input(type="radio" value="6" v-model="position")
            span 人資職

    button(type="submit") 提交問卷
</template>

<style scoped>
.error {
  color: red;
  font-size: 0.8em;
  margin-left: 10px;
}
</style>