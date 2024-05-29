<template>
  <v-app>
    <v-main>
      <router-view />





    <!-- <div>
      <div class="text-center d-flex pb-4">
        <v-btn class="ma-2" @click="all">
          All
        </v-btn>
        <v-btn class="ma-2" @click="none">
          None
        </v-btn>
      </div>

    <div class="pb-4">v-model {{ panel }}</div>
      <v-expansion-panels
      v-model="panel"
      multiple
    >
      <v-expansion-panel
        text="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
        title="Foo"
        value="foo"
      >
      <form @submit.prevent>
          <h4>add guests</h4>
          <input 
            v-bind:value="guest_name"
            @input="guest_name = $event.target.value"
            class="input"
            type="text"
            placeholder="Name"
          >
          <button class="from_mybttn" @click="addguest">add</button>
        </form>

        <div class = "position__cost" v-for="guest in guests">
          <div><strong>Guest {{ guest.id }}:</strong> {{ guest.guest_name }}</div>
        </div>
      </v-expansion-panel>

      <v-expansion-panel
        text="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
        title="Bar"
        value="bar"
      ></v-expansion-panel>

      <v-expansion-panel
        text="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
        title="Baz"
        value="baz"
      ></v-expansion-panel>
    </v-expansion-panels>
    </div> -->





      
      <div class="cont">
        <!-- <home-page></home-page> -->
        <!-- <div class="move">
          <my-button class="move__btn">home</my-button>
          <my-button class="move__btn">help</my-button>
        </div>
        <div>Welcome to "Divide the bill" app!</div>
        <div>Click "next step" button to go forward</div>
        <my-button class="btn__bottom">next step</my-button> -->

        <!-- Здесь мы добавляем человеков -->
        <!-- @submit.prevent предотвращает обновление страницы после отправки формы -->
        <form @submit.prevent>
          <h3>add guests</h3>
          <input 
            v-bind:value="guest_name"
            @input="guest_name = $event.target.value"
            class="input"
            type="text"
            placeholder="Name"
          >

          <!-- Кнопочки оформить -->
          <button class="from_mybttn" @click="addguest">add</button>
        </form>
        <div class = "guest__flex">
          <div class = "guest__container" v-for="guest in guests" :key="guest.id">
            <div>{{ guest.guest_name }}</div>
          </div>
        </div>

        <!-- Здесь мы добавляем позицию и её стоимость -->
        <!-- @submit.prevent предотвращает обновление страницы после отправки формы -->
        <form @submit.prevent> 
          <h3>add menu positions</h3>
          <!-- Позиция меню -->
          <input 
            v-bind:value="dish" 
            @input="dish = $event.target.value" 
            class="input" 
            type="text" 
            placeholder="Menu position"
          >
          <!-- Стоимость -->
          <input 
            v-bind:value="dish_cost" 
            @input="dish_cost = $event.target.value" 
            class="input"
            type="number" 
            placeholder="Cost"
          >

          <!-- Кнопочки оформить -->
          <button class="from_mybttn" @click="addPosition">add</button>
        </form>

        <div v-for="dish in dishes">
          <div class = "position__cost">
            <div><strong>Menu position:</strong> {{ dish.dish }} </div> 
            <div><strong>Cost:</strong> {{ dish.dish_cost }} </div> 
            <div><strong>Who ate?</strong> 
              <div class = "" v-for="guest in guests">
                <div>{{ guest.guest_name }}</div>
                <input type="checkbox" value="guest.guest_name" v-model="checkedNames" />
              </div>
            </div>
          </div>
        </div>

        <!-- Просто всякие доп элементы, которые потом надо будет преобразовать -->
        <!-- <guest-form></guest-form>
        <guest-list></guest-list>
        <bill-result></bill-result>
        <debt-list></debt-list> -->
        <h3>The total is: {{ this.totally }}</h3>


        
      </div>
    </v-main>
  </v-app>
</template>

<script>
import HomePage from "./components/HomePage.vue";
import GuestList from "./components/GuestList.vue";
import DebtList from "./components/DebtList.vue";
import SpendingList from "./components/SpendingList.vue";
import BillResult from "./components/BillResult.vue";
import GuestForm from "./components/GuestForm.vue";
import MyButton from "./components/UI/MyButton.vue";


export default {
  components: {
    HomePage,
    GuestList,
    DebtList,
    SpendingList,
    BillResult,
    GuestForm,
    MyButton


  },
  data() {
    return {
      guests: [
        // {id: 1, guest_name: 'Anton'},
        // {id: 2, guest_name: 'Ann'},
        // {id: 3, guest_name: 'Serj'},
      ],

      dishes: [
        { dish:'', dish_cost: 0, eatenBy:[]},
        // {idf: 1, dish: 'Steak', dish_cost: '1000', eatenby: []},
        // {idf: 2, dish: 'Fruit salad', dish_cost: '500'},
        // {idf: 3, dish: 'Whiskey', dish_cost: '7000'},
      ],
      dish: '',
      dish_cost: '',
      panel: [],
      bill: '',
      total: [],
      totally: 0,
      eatenBy: [],
    }
  },
  methods: {
    addguest () {
      const newguest = {
        id: Date.now(),
        guest_name: this.guest_name,
      }
      if (this.guest_name!=='') 
        {
          this.guests.push(newguest);
          this.resetForm();
        } else {
          alert('The form is empty. There should be at least one character.')
        }
    },
    resetForm() {
      this.guest_name = '';
      this.dish = '';
      this.dish_cost = '';
    },

    addPosition () {
      const newPosition = {
        id: Date.now(),
        dish: this.dish,
        dish_cost: this.dish_cost,
      }
      if (this.dish!=='' && this.dish_cost!==0 && this.dish_cost > 0) 
        {
          this.totally = this.totally + parseInt(this.dish_cost);
          this.dishes.push(newPosition);
          this.total.push(this.dish_cost);
          this.resetForm();
        } else if (this.dish=='' || this.dish_cost=='') {
          alert('One or both of the forms are empty. There should be at least one character or digit.')
        } else if (this.dish_cost <= 0) {
          alert("The cost can be only greater than zero.")
        }
      
    },

    // all () {
    //     this.panel = ['foo', 'bar', 'baz']
    //   },
    // none () {
    //     this.panel = []
    //   },
    getGuestWhoAteDish(guestsIds) {
        return this.guests.filter(guest => guestsIds.includes(guest.id));
    },
  }

}

</script>

<style scoped>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.input {
  display: flex;
  margin-bottom: 7%;
  margin-top: 7%;   
  border: 1px solid brown;
  padding: 2px 5px;
  color: black;
}

.cont {
  /* margin: auto; */
  /* position: sticky; */
  /* top: 50%;
  left: 50%; */
  transform: translate(75%, 0%);
  background-color: white;
  /* box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Горизонтальное смещение, вертикальное смещение, размытие, цвет тени */
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 40%;
  /* height: auto; */
  text-align: center;
  color: black;
  margin-top: -850px;
}

.guest__container {
  display: flex;
  border: 1px solid;
  background-color: blanchedalmond;
  height: 105%;
  width: 100%;
  padding: 2%;
  align-items: center;
  justify-content: center;
  /* margin-top: 4%;
  margin-bottom: 4%; */
  margin: 3%;
}

.guest__flex {
  display: flex;
  flex-direction: row;
  width: 100%;
  flex-wrap: wrap;  
}

.btn__bottom {
  background-color: rgb(94, 61, 31);
  color: white;
  border-radius: 7px;
  padding: 5px;
  padding-left: 20px;
  padding-right: 20px;
  margin-top: 150px;

}
.move {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 15px;
}


.move__btn {
  background-color: rgb(94, 61, 31);
  color: white;
  font-size: 13px;
  border-radius: 7px;
  padding: 5px;
  padding-left: 15px;
  padding-right: 15px;
}

.position__cost {
  display: flex;
  border: 1px solid;
  background-color: blanchedalmond;
  height: 105%;
  width: 100%;
  padding: 2%;
  align-items: flex-start;
  justify-content: flex-start;
  flex-direction: column;
  margin-top: 4%;
  margin-bottom: 4%;
}

.from_mybttn {
  padding: 8px 23px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

</style>