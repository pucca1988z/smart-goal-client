<template>
  <div class=" pr-4  bg-white font-mono rounded-lg m-4 shadow-xl">
    <div class="flex flex-row">
      <div class="flex-1 relative"  >
        <div 
          :style="{backgroundImage:`url(${require('@/assets/picForA.jpg')}`, filter:`blur(3px) grayscale(50%)` }"
          class="bg-cover bg-no-repeat bg-center h-full  rounded-tl-lg rounded-bl-lg ">
          <div class=" absolute  bg-black opacity-40 h-full w-full  text-white text-l" style="">
          </div>
        </div>
        <div class=" absolute text-white top-1/3 w-full ">
          <div class="border mx-8 px-4 py-2">
            <div class="text-3xl">
              {{reminder.standFor}} 
            </div>
            <div class="text-xl">
              {{reminder.reminderContent}}
            </div>
          </div>
        </div>

      </div>
      <div class="w-2/3">
        <div class="grid grid-cols-3 gap-6 space-y-4 py-4 pl-6">
          <div class=" col-span-2 text-2xl text-gray-400 -mb-8">Create Goal</div>
          <div class=" col-span-3">
            <label for="company_website" class=" capitalize  block text-2xl font-medium text-gray-700">
              your goal name?
            </label>
            <input 
              @focus="onInputClick('s')"
              v-model="specificGoalName"
              type="text" 
              class=" w-full border-b-2 sm:text-sm outline-none focus:border-blue-500 transition duration-500"
              placeholder="Try to make it simple, sensible and significant."  
            >
          </div>

          <div class="col-span-3">
            <label for="about" class="capitalize block text-2xl font-medium text-gray-700">
              how to measure it?
            </label>
            <input 
              @focus="onInputClick('m')"
              v-model="measurableGoal"
              type="text"
              class=" w-full border-b-2 sm:text-sm outline-none focus:border-blue-500 transition duration-500"
              placeholder="How will you know when it is accomplished?"  
            >
          </div>

          <div class="col-span-3">
            <label for="about" class="capitalize block text-2xl font-medium text-gray-700">
              is your goal achievable?
            </label>
            <input 
              @focus="onInputClick('a')"
              v-model="achievableGoal"
              type="text"
              class=" w-full border-b-2 sm:text-sm outline-none focus:border-blue-500 transition duration-500"
              placeholder="Mind that your goal needs to be realistic and attainable to be successful. "  
            >
          </div>

          <div class="col-span-3">
            <label for="about" class="capitalize block text-2xl font-medium text-gray-700">
              Does this match our other efforts/needs?
            </label>
            <input 
              @focus="onInputClick('r')"
              v-model="relevantGoal"
              type="text"
              class=" w-full border-b-2 sm:text-sm outline-none focus:border-blue-500 transition duration-500">
          </div>

          <div class="col-span-3">
            <label for="about" class="capitalize block text-2xl font-medium text-gray-700">
              Set yourself a target date:
            </label>
            <DatePicker  
              @focus="onInputClick('t')"
              valueType="format"
              range class="w-full shadow" v-model="timeBound"/>
          </div>

          <div @click="onSubmitClick" class="border rounded-3xl cursor-pointer col-start-3 text-center hover:bg-gray-700 text-white bg-gray-500  transition duration-500">
            Submit
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker'
import 'vue2-datepicker/index.css'
import axios from 'axios'


export default {
  components:{
    DatePicker
  },
  data(){
    return {
      specificGoalName:"",
      measurableGoal:"",
      achievableGoal:"",
      relevantGoal:"",
      timeBound:"",
      time3:null,
      reminder:{
        standFor:"", reminderContent:"", imageUrl:""
      },
      SMART:{
        s:{
          standFor:"Specific",
          reminderContent: "Your goal should be clear and specific, otherwise you won't be able to focus your efforts or feel truly motivated to achieve it.",
          imgUrl:"@/src/assets/picForS.jpg",
        },
        m:{
          standFor:"Measurable" ,
          reminderContent:"Set a measurable goals, so that you can track your progress and stay motivated.",
          imgUrl:"@/src/assets/picForM.jpg",
        },
        a:{
          standFor:"Achievable" ,
          reminderContent:"Your goal also needs to be realistic and attainable to be successful. It should stretch your abilities but still remain possible. ",
          imgUrl:"@/src/assets/picForA.jpg",
        },
        r:{
          standFor:"Relevant" ,
          reminderContent:"This step is about ensuring that your goal matters to you, and that it also aligns with other relevant goals. ",
          imgUrl:"@/src/assets/picForR.jpg",
        },
        t:{
          standFor:"Time-bound" ,
          reminderContent:"Every goal needs a target date, so that you have a deadline to focus on and something to work toward. ",
          imgUrl:"@/src/assets/picForT.jpg",
        }
      }
    }
  },
  watch:{},
  mounted(){
    this.onInputClick('s')
  },
  methods:{
    onInputClick(type){
      this.reminder.standFor = this.SMART[type].standFor
      this.reminder.reminderContent = this.SMART[type].reminderContent
      this.reminder.imgUrl = this.SMART[type].imgUrl      
    },
    onSubmitClick(){
      axios.post('http://localhost:5000/goals',{
        specificGoalName:this.specificGoalName,
        measurableGoal:this.measurableGoal,
        achievableGoal:this.achievableGoal,
        relevantGoal:this.relevantGoal,
        timeBound:this.timeBound
      })
      .then( res => {
        this.initData();
      })
    },
    initData(){
      this.specificGoalName = '';
      this.measurableGoal = '';
      this.achievableGoal = '';
      this.relevantGoal = '';
      this.timeBound = null;
    }
  }
}
</script>

