<template>
  <div id="app">
    <div class="container">
        <div class="row first">
          <div class="col-md-4">
            <div class="users-listing">
              <div class="search-wrapper">
                <input class="form-control" type="text" v-model="searchQuery" placeholder="Search">
              </div>
            <h4 class="user-title">List of Users</h4>
              <ul>
                <li v-for="(user, index) in users" :key="index">
                  <p @click="viewUserListing(user, index)" :class="{'active': user.id == isActive}">{{ user.first_name }}<span>{{ user.last_name }}</span></p>
                </li>
              </ul>
              <table>
                <thead>
                  List of Content
                </thead>
                <tbody>
                  <tr v-for="(item, index) in resultQuery" :key="index">
                    <td>{{ item.title }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          <div class="col-md-8 user-col-details">
            <div class="display-users-details">
              <div class="row">
                <div class="col-12 inner-form-detail">
                  <p>User ID: {{ selectedUser.id }}</p>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>First Name</label>
                  <input type="text" v-model="selectedUser.first_name"/>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Last Name</label>
                  <input type="text" v-model="selectedUser.last_name"/>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Email</label>
                  <input type="email" v-model="selectedUser.email"/>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Address</label>
                  <input type="text" v-model="selectedUser.address"/>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Gender</label>
                  <div class="gender-sec">
                    <input type="radio" id="fogender" v-model="selectedUser.gender" value="Male"/>
                    <label for="fogender">Male</label>
                    <input type="radio" id="fogender" v-model="selectedUser.gender" value="Female"/>
                    <label for="fogender">Female</label>
                  </div>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Phone Number</label>
                  <input type="text" v-model="selectedUser.phone"/>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Language Spoken</label>
                  <select v-model="selectedUser.language_spoken">
                    <option v-for="(list, index) in users" :key="index" :value="list.language_spoken">{{ list.language_spoken }}</option>
                  </select>
                </div>
                <div class="col-md-6 inner-form-detail">
                  <label>Your Interests</label>
                  <div v-for="(hobby, index) in interests" :key="index" class="yourHobbies">
                    <div>
                      <input type="checkbox" :id="hobby + index" v-model="selectedUser.interest" :value="hobby"/>
                      <label :for="hobby + index">{{ hobby }}</label>
                    </div>
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-md-12">
                  <div class="manipulation-buttons">
                    <ul>
                      <li><button class="btn btn-primary" @click="addUsers()">Add Name</button></li>
                      <li><button class="btn btn-success" @click="updateUsers()">Update</button></li>
                      <li><button class="btn btn-danger" @click="deleteUsers()">Delete</button></li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
import Popup from './component/Popup'

export default {
  name: 'app',
  components: {
    Popup
  },
  data() {
    return {
      searchQuery: null,
      users: [
            {id: '1',first_name: 'Colas', last_name: 'Bailes', email: 'cbailes0@canalblog.com', address: '52286 Farmco Parkway', gender: 'Male', phone: '558-120-3371', language_spoken: 'Finnish', interest:['Coding', 'Everything']},
            {id: '2',first_name: 'Inigo', last_name: 'Guiel', email: 'iguiel1@zdnet.com', address: '0 Kings Park', gender: 'Male', phone: '400-753-8346', language_spoken: 'Kashmiri', interest:['Football']},
            {id: '3',first_name: 'Erminie', last_name: 'St Pierre', email: 'estpierre2@seesaa.net', address: '3113 High Crossing Crossing', gender: 'Female', phone: '369-262-7525', language_spoken: 'Haitian Creole', interest:['Coding']},
            {id: '4',first_name: 'Pauletta', last_name: 'Bandiera', email: 'pbandiera3@ebay.com', address: '73778 Lien Court', gender: 'Female', phone: '499-266-2581', language_spoken: 'Korean', interest:['Everything']},
            {id: '5',first_name: 'Renae', last_name: 'Strainge', email: 'rstrainge4@cisco.com', address: '197 Jenna Point', gender: 'Female', phone: '992-715-3250', language_spoken: 'Oriya', interest:['Nothing']},
            {id: '6',first_name: 'Horatio', last_name: 'Berrygun', email: 'hberrygun5@skyrock.com', address: '37 Pepper Wood Place', gender: 'Male', phone: '807-712-8166', language_spoken: 'Romanian', interest:['Sleeping']},
            {id: '7',first_name: 'Laryssa', last_name: 'Pugsley', email: 'lpugsley6@dmoz.org', address: '37 Toban Alley', gender: 'Female', phone: '740-622-8952', language_spoken: 'Korean', interest:['Coding']},
            {id: '8',first_name: 'Peggy', last_name: 'Ramsay', email: 'pramsay7@arstechnica.com', address: '95 Almo Point', gender: 'Female', phone: '933-472-5866', language_spoken: 'Chinese', interest:['Sleeping']},
            {id: '9',first_name: 'Kanya', last_name: 'Bloor', email: 'kbloor8@addtoany.com', address: '8 Heath Terrace', gender: 'Female', phone: '917-712-2669', language_spoken: 'Oriya', interest:['Nothing']},
            {id: '10',first_name: 'Justinn', last_name: 'Farmar', email: 'jfarmar9@ibm.com', address: '777 Mandrake Crossing', gender: 'Female', phone: '789-773-2735', language_spoken: 'Persian', interest:['Chating']},
            {id: '11',first_name: 'Bertrand', last_name: 'Seagar', email: 'bseagara@themeforest.net', address: '296 Spaight Terrace', gender: 'Male', phone: '403-752-5360', language_spoken: 'Nepali', interest:['Gaming']},
            {id: '12',first_name: 'Vincenz', last_name: 'Prescot', email: 'vprescotb@earthlink.net', address: '479 Melvin Way', gender: 'Male', phone: '835-884-5863', language_spoken: 'Icelandic', interest:['Football']},
            {id: '13',first_name: 'Perceval', last_name: 'Flanner', email: 'pflannerc@netvibes.com', address: '290 Loeprich Crossing', gender: 'Male', phone: '111-405-5713', language_spoken: 'Malayalam', interest:['Coding']},
            {id: '14',first_name: 'Jonathon', last_name: 'Gonnelly', email: 'jgonnellyd@google.com.au', address: '32680 Bluestem Pass', gender: 'Male', phone: '289-843-9329', language_spoken: 'Tsonga', interest:['Sports']},
            {id: '15',first_name: 'Kristin', last_name: 'Ratazzi', email: 'kratazzie@timesonline.co.uk', address: '78 Golf View Street', gender: 'Female', phone: '456-922-8285', language_spoken: 'Maltese', interest:['Art']},
            {id: '16',first_name: 'Viki', last_name: 'McIlrath', email: 'vmcilrathf@smugmug.com', address: '117 Moulton Lane', gender: 'Female', phone: '716-277-5628', language_spoken: 'Hindi', interest:['Coding']},
            {id: '17',first_name: 'Arlene', last_name: 'Fessions', email: 'afessionsg@go.com', address: '29 Crownhardt Junction', gender: 'Female', phone: '577-802-1477', language_spoken: 'Quechua', interest:['Everything']},
            {id: '18',first_name: 'Putnem', last_name: 'Forshaw', email: 'pforshawh@paginegialle.it', address:'472 Bonner Road', gender: 'Male', phone: '335-502-4195', language_spoken: 'Pashto', interest:['Nothing']},
            {id: '19',first_name: 'Karrah', last_name: 'Schutter', email: 'kschutteri@vk.com', address: '467 Oxford Lane', gender: 'Female', phone: '208-879-0156', language_spoken: 'Tajik', interest:['Sports']},
            {id: '20',first_name: 'Gordie', last_name: 'Blackbourn', email: 'gblackbournj@tumblr.com', address: '54 Esch Crossing', gender: 'Male', phone: '931-743-8217', language_spoken: 'Norwegian', interest:['Art']},
            {id: '21',first_name: 'Berte', last_name: 'Wickens', email: 'bwickensk@google.com.hk', address: '258 Marcy Hill', gender: 'Female', phone: '333-289-4253', language_spoken: 'English', interest:['Music']}
        ],
        interests: ['Coding', 'Football', 'Everything', 'Nothing', 'Art', 'Sleeping', 'Chating', 'Gaming', 'Sports', 'Music'],
      selectedUser: {
        interest: [],
      },
       event: {id: '',first_name: '', last_name: '', email: '', address: '', gender: '', phone: '', language_spoken: '', interest:[]},
      isActive: '',
      isActiveIndex: ''
    }
  },
  methods: {
    viewUserListing: function(user, index) {
      console.log(user);
      this.selectedUser = user;
      // console.log(this.selectedUser);

      this.isActive = user.id;
      this.isActiveIndex = index;
    },
    addUsers: function(){
      this.users.push(this.selectedUser);
      alert("Name Added Successfully");
    },
    updateUsers: function(){
      // console.log(this.isActiveIndex);
    },
    deleteUsers: function(){
      console.log(this.isActiveIndex);
      this.users.splice(this.isActiveIndex, 1);
      
    }
    // showMsgBoxTwo() {
    //     this.boxTwo = ''
    //     this.$bvModal.msgBoxConfirm('Please confirm that you want to delete everything.', {
    //       title: 'Please Confirm',
    //       size: 'sm',
    //       buttonSize: 'sm',
    //       okVariant: 'danger',
    //       okTitle: 'YES',
    //       cancelTitle: 'NO',
    //       footerClass: 'p-2',
    //       hideHeaderClose: false,
    //       centered: true
    //     })
    //       .then(value => {
    //         this.boxTwo = value
    //       })
    //       .catch(err => {
    //         // An error occurred
    //       })
    //   }
  },
  computed: {
    resultQuery() {
      if(this.searchQuery) {
        // return this.users.filter((item) =>{
        //   return this.searchQuery.control.toLowerCase().split(' ').every(v => item.titile.toLowerCase().includes(v))
        // })
        console.log(this.searchQuery);
      } else {
        return this.users;
      }
    }
  }
}
</script>

<style lang="scss">
body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  
}
#app .row.first {
    box-shadow: 0 0 20px rgba(0,0,0,.2)!important;
    margin: 40px 0;
    border-radius: 20px;

    .users-listing {
      padding: 40px 0px;
      .search-wrapper {
        margin-bottom: 20px;

        .form-control{
          border: 1px solid #000000;
        }
      }

      h4 {
        margin-bottom: 15px;
        padding-left: 15px;
      }
      ul {
        margin-bottom: 0;
        padding: 0;
        height: 100vh;
        overflow: scroll;

        li {
          margin-bottom: 4px;
          list-style: none;
            &:hover, &:focus {
                cursor: pointer;
                background: #f8f9fa;
            }
            &:last-child {
              margin-bottom: 0;
            }

          p {
            margin-bottom: 0;
            padding: 10px 15px;

            span {
              display: block;
            }
          }
          p.active {
            color: #ffffff;
            background: #6b6b6b;
          }
        }
      }
    } 
    .user-col-details {
      border-radius: 0 20px 20px 0;
      padding: 25px 40px 40px;
      background: #f5f5f5;

      .display-users-details {
        .inner-form-detail{
          margin: 15px 0;
          label {
            display: block;
            font-size: 18px;
            margin-bottom: .5rem;
            color: #999;
          }
          input[type="text"], input[type="email"], select {
            border-radius: 20px;
            width: 100%;
            padding: .375rem .75rem;
            font-size: 1rem;
            font-weight: 400;
            line-height: 1.5;
            height: 60px;
            color: #999999;
            background-color: #fff;
            background-clip: padding-box;
            border: 1px solid #ced4da;
            transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;

            &:focus {
              outline: none;
              border: 2px solid #000000;
              border-radius: 20px;
            }
          }
          select > option {
            font-size: 18px;
            padding: 5px 0;
          }
          .gender-sec {
            display: flex;
            align-items: center;

            label {
              margin: 0 10px;
            }
            input[type="radio"] {
              margin-left: 10px;
            }
          }
        }
    }
    .yourHobbies {
      display: inline-block;
      div {
        display: flex;
        align-items: center;
        margin: 0 10px 5px;

        label {
          margin: 0 20px 0 10px !important;
        }
      }
    }
    .manipulation-buttons {
      ul {
        display: flex;
        justify-content: space-between;
        margin: 50px 0 0;
        padding: 0;

        li {
          list-style: none;

          button.btn {
            padding: 12px 60px;
            min-width: 180px;
            font-size: 18px;
          }
        }
      }
    }
  }
}

</style>
