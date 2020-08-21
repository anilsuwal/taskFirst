<template>
  <div id="app">
    <div class="container">
        <div class="row first">
          <div class="col-md-4">
            <h4 class="user-title">List of Users</h4>
            <div class="users-listing">
              <ul>
                <li v-for="(user, index) in users" :key="index">
                  <p @click="viewUserListing(index)" :class="{'active': index == isActive}">{{ user.first_name }}</p>
                </li>
              </ul>
            </div>
          </div>
          <div class="col-md-8 user-col-details">
            <div class="display-users-details">
              <p>{{ selectedUser.first_name }}</p>
              <p></p>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      users: [
            {id: '1',first_name: 'Colas', last_name: 'Bailes', email: 'cbailes0@canalblog.com', address: '52286 Farmco Parkway', gender: 'Male', phone: '558-120-3371', language_spoken: 'Finnish'},
            {id: '2',first_name: 'Inigo', last_name: 'Guiel', email: 'iguiel1@zdnet.com', address: '0 Kings Park', gender: 'Male', phone: '400-753-8346', language_spoken: 'Kashmiri'},
            {id: '3',first_name: 'Erminie', last_name: 'St Pierre', email: 'estpierre2@seesaa.net', address: '3113 High Crossing Crossing', gender: 'Female', phone: '369-262-7525', language_spoken: 'Haitian Creole'},
            {id: '4',first_name: 'Pauletta', last_name: 'Bandiera', email: 'pbandiera3@ebay.com', address: '73778 Lien Court', gender: 'Female', phone: '499-266-2581', language_spoken: 'Korean'},
            {id: '5',first_name: 'Renae', last_name: 'Strainge', email: 'rstrainge4@cisco.com', address: '197 Jenna Point', gender: 'Female', phone: '992-715-3250', language_spoken: 'Oriya'},
            {id: '6',first_name: 'Horatio', last_name: 'Berrygun', email: 'hberrygun5@skyrock.com', address: '37 Pepper Wood Place', gender: 'Male', phone: '807-712-8166', language_spoken: 'Romanian'},
            {id: '7',first_name: 'Laryssa', last_name: 'Pugsley', email: 'lpugsley6@dmoz.org', address: '37 Toban Alley', gender: 'Female', phone: '740-622-8952', language_spoken: 'Korean'},
            {id: '8',first_name: 'Peggy', last_name: 'Ramsay', email: 'pramsay7@arstechnica.com', address: '95 Almo Point', gender: 'Female', phone: '933-472-5866', language_spoken: 'Chinese'},
            {id: '9',first_name: 'Kanya', last_name: 'Bloor', email: 'kbloor8@addtoany.com', address: '8 Heath Terrace', gender: 'Female', phone: '917-712-2669', language_spoken: 'Oriya'},
            {id: '10',first_name: 'Justinn', last_name: 'Farmar', email: 'jfarmar9@ibm.com', address: '777 Mandrake Crossing', gender: 'Female', phone: '789-773-2735', language_spoken: 'Persian'},
            {id: '11',first_name: 'Bertrand', last_name: 'Seagar', email: 'bseagara@themeforest.net', address: '296 Spaight Terrace', gender: 'Male', phone: '403-752-5360', language_spoken: 'Nepali'},
            {id: '12',first_name: 'Vincenz', last_name: 'Prescot', email: 'vprescotb@earthlink.net', address: '479 Melvin Way', gender: 'Male', phone: '835-884-5863', language_spoken: 'Icelandic'},
            {id: '13',first_name: 'Perceval', last_name: 'Flanner', email: 'pflannerc@netvibes.com', address: '290 Loeprich Crossing', gender: 'Male', phone: '111-405-5713', language_spoken: 'Malayalam'},
            {id: '14',first_name: 'Jonathon', last_name: 'Gonnelly', email: 'jgonnellyd@google.com.au', address: '32680 Bluestem Pass', gender: 'Male', phone: '289-843-9329', language_spoken: 'Tsonga'},
            {id: '15',first_name: 'Kristin', last_name: 'Ratazzi', email: 'kratazzie@timesonline.co.uk', address: '78 Golf View Street', gender: 'Female', phone: '456-922-8285', language_spoken: 'Maltese'},
            {id: '16',first_name: 'Viki', last_name: 'McIlrath', email: 'vmcilrathf@smugmug.com', address: '117 Moulton Lane', gender: 'Female', phone: '716-277-5628', language_spoken: 'Hindi'},
            {id: '17',first_name: 'Arlene', last_name: 'Fessions', email: 'afessionsg@go.com', address: '29 Crownhardt Junction', gender: 'Female', phone: '577-802-1477', language_spoken: 'Quechua'},
            {id: '18',first_name: 'Putnem', last_name: 'Forshaw', email: 'pforshawh@paginegialle.it', address:'472 Bonner Road', gender: 'Male', phone: '335-502-4195', language_spoken: 'Pashto'},
            {id: '19',first_name: 'Karrah', last_name: 'Schutter', email: 'kschutteri@vk.com', address: '467 Oxford Lane', gender: 'Female', phone: '208-879-0156', language_spoken: 'Tajik'},
            {id: '20',first_name: 'Gordie', last_name: 'Blackbourn', email: 'gblackbournj@tumblr.com', address: '54 Esch Crossing', gender: 'Male', phone: '931-743-8217', language_spoken: 'Norwegian'},
            {id: '21',first_name: 'Berte', last_name: 'Wickens', email: 'bwickensk@google.com.hk', address: '258 Marcy Hill', gender: 'Female', phone: '333-289-4253', language_spoken: 'English'}
        ],
      selectedUser: {

      },
      isActive: 0
    }
  },
  methods: {
    viewUserListing: function(index1) {
      console.log(index1);
      this.selectedUser = this.users[index1];
      console.log(this.selectedUser);

      this.isActive = index1;
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
    padding: 40px 20px;

    .users-listing {
      ul {
        margin-bottom: 0;
        padding: 0;

        li {
          margin-bottom: 14px;
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
            padding: 12px 10px;
          }
          p.active {
            color: #ffffff;
            background: #6b6b6b;
          }
        }
      }
    } 
    .user-col-details {
      background: #f5f5f5;
  }
}

</style>
