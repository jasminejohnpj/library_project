<template>
    <div>
        <div class="pa-6">
  <v-card>
    <v-toolbar
      color="cyan"
      dark
      flat
    >
    <v-tabs
    v-model="memberStatus"
        centered
        slider-color="yellow"
        background-color="transparent"
        class="hidden-xs-only">

        <v-tab  class="mx-auto"
    color="secondary"
    width="200px">
          Membership Requests
        </v-tab>

        <v-tab>
          Members
        </v-tab>
        </v-tabs>
      </v-toolbar>
      
  <v-tabs-items v-model="memberStatus">
    </v-tabs-items>
    
  </v-card>
    </div>
   <v-card>
                <v-card-title>
                  {{ getUsers.firstName }}
                </v-card-title>
                <v-card-text>{{ getUsers.wardNumber }}</v-card-text>
              </v-card>
    <!-- <template v-for="(item,index) in getUsers">
          
          <v-list-item  :key="item.cardNumber">
            <v-list-item-avatar>
              <v-img src="https://cdn.vuetifyjs.com/images/parallax/material.jpg"></v-img>
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title v-text="item.firstName"></v-list-item-title>
            <h6>Card Number : {{item.cardNumber}}</h6>
            
            </v-list-item-content> -->
              <!-- <v-btn 
              color="secondary" @click="getSelectedData(item)">View</v-btn>
              &nbsp;&nbsp;
              <v-btn 
              color="secondary" @click="getDeleteData(item)">Delete</v-btn> -->
          <!-- </v-list-item>
          <v-divider :key="index" :inset="true"></v-divider>
        </template>
      -->


      <!-- <v-list three-line class="pa-6" v-else> 
        <member-ship-list></member-ship-list>
      </v-list> -->



    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <v-card>
        <v-card-title>
          <span class="text-h5">Member Profile</span>
        </v-card-title>
        <v-card-text>
          
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="First name"
                  v-model="firstName"
             
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Last name"
                  v-model="lastname"
                 
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="District"
                  v-model="district"
             
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="House name"
                  v-model="houseName"
             
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Post office"
                  v-model="postOffice"
                 
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Postal code"
                  v-model="postalCode"
                 
                ></v-text-field>
              </v-col>
              <v-col
               cols="12"
               sm="8"
                md="5">
                
                <v-text-field
                  label="Email"
                  v-model="email"
               
                ></v-text-field>
              </v-col>
              <v-col cols="12"
              sm="6">
                <v-text-field
                  label="Phone number"
                  v-model="phoneNumber"
               
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Gender"
                  v-model="gender"
            
                ></v-text-field>
              </v-col>
               <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Card number"
                  v-model="cardNumber"
             
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Ward number"
                  v-model="wardNumber"
                 
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Ward name"
                  v-model="wardName"
             
                ></v-text-field>
              </v-col>

              <v-col
                cols="12"
                sm="6"
                md="4"
              >
              <v-text-field
                  label="Category "
                  v-model="category"
                  
                ></v-text-field>
             
                </v-col>
                <v-col
                cols="12"
                sm="6"
                md="4"
              >
              <v-select
                  :items="items"
                  label="Type of Membership"                
                  required
                  v-model="typeofmembership"
                ></v-select>
            </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Date of birth"
                  v-model="dataOfBirth" 
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Date Of Entry"
                  v-model="dateofentry"
                  input type="date"
                   >
                  </v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Expiry Date"
                  v-model="expirydate"
                  input type="date"
                ></v-text-field>
              </v-col>
            </v-row>
           
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
           Update
        </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog
      v-model="errorAlert"
      persistent
      max-width="290"
    >
        <v-card> 
          <v-card-title class="text-h5">
          Error Message
        </v-card-title>
        <v-card-text> {{errorMsg}}</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="errorAlert=false"
          >
            Okay
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog
      v-model="deleteAlert"
      persistent
      max-width="290"
    >
        <v-card> 
          <v-card-title class="text-h5">
          Confirm Delete
        </v-card-title>
        <v-card-text> Are you sure you want to delete the user?</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="deleteAlert = false"
          >
            No
          </v-btn>
          <v-btn
            color="red darken-1"
            text
            @click="callDeleteUser(items)"
          >
            Yes
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    </div>
</template>

<script> 
import axios from 'axios'
export default{
    data(){
        return{
            memberStatus:false,
            cardNumber:'',
            firstName:'',
            lastname:'',
            district:'',
            houseName:'',
            postOffice:'',
            postalCode:'',
            email:'',
            phoneNumber:'',
            gender:'',
            cardNumber:'',
            wardNumber:'',
            wardName:'',
            category:'',
            typeofmembership:'',
            items:[],
            dataOfBirth:'',
            dateofentry:'',
            expirydate:'',
            errorAlert:false,
            errorMsg:'',
            dialog:false,
            deleteAlert:false,
            getUsers:[]
        }
    },
    mounted() {
        this.memberslist;
    },
    methods: {
        async memberslist()
        {
            try{
                const response = await axios.get(`${process.env.apiUrl}admin/get_all_valid_users`);
                const getUsers = response.data;
                console.log(response);
                getUsers.docs.forEach((e,i)=> {

                console.log(e,i,e._id)
  
                    }); 
                
            }
            catch (error) {
                console.error("Error fetching members list", error);
                this.showSnackBar("Error fetching members list.");
}
        }
    }
}
</script>