<template>
  <div>
    <v-snackbar v-model="snackAlert">
      Order Placed successfully
      <template v-slot:action="{ attrs }">
        <v-btn color="pink" text v-bind="attrs" @click="snackAlert = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <v-form @submit.prevent="createUser" ref="form">
      <v-dialog v-model="dialog" persistent max-width="600px">
        <v-card>
          <v-card-title>
            <span class="text-h5">Book Request</span>
          </v-card-title>
          <v-card-text>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Title"
                  v-model="title"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Author"
                  v-model="author"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="accessionNo*"
                  v-model="accessionNo"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Call No"
                  v-model="callno"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="cardNumber*"
                  v-model="cardNumber"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Shelf No*"
                  v-model="shelfno"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Subject/type of Book:"
                  v-model="subjecttypeofbook"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Barcode*"
                  v-model="barCode"
                  required
                  :rules="numberRules"
                ></v-text-field>
                <small>*Barcode should be unique and cannot be editable.</small>
              </v-col>
            </v-row>

            <hr />

            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Username*"
                  v-model="userName"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Housename*"
                  v-model="houseName"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Wardname*"
                  v-model="wardName"
                  required
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="PostOffice*"
                  v-model="postOffice"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Phone number*"
                  v-model="phoneNumber"
                  required
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>

            <small>*indicates required field</small>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="clearData"> Close </v-btn>
            <v-btn color="blue darken-1" text @click="checkOut"> Accept </v-btn>
            <v-btn color="blue darken-1" text @click="checkOut"> Update </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-form>

    <v-list three-line v-if="getHoldList.length !== 0">
      <template v-for="(item, index) in getHoldList">
        <v-list-item :key="item._id">
          <v-list-item-avatar>
            <!-- <v-img :src="imageLink + item.bibiloId"></v-img> -->
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-text="item.bookName"></v-list-item-title>

            <v-list-item-subtitle
              v-text="item.accessionNo"
            ></v-list-item-subtitle>
          </v-list-item-content>
          <v-btn color="secondary" >View</v-btn>
          &nbsp;&nbsp;
          <v-btn color="secondary" >Cancel</v-btn>
        </v-list-item>
        <v-divider :key="index" :inset="true"></v-divider>
      </template>
    </v-list>
  </div>
</template>

<script>
export default {
  data: () => ({
    numberRules: [
      (v) => !!v || "Barcode is required",
      (v) => (v && v.length >= 1) || "Number should be valid",
    ],
    bibiloIds:[],
    dialog: false,
    title: "",
    author: "",
    accessionNo: "",
    callno: "",
    cardNumber: "",
    shelfno: "",
    subjecttypeofbook: "",
    barCode: "",
    userName: "",
    houseName: "",
    wardName: "",
    postOffice: "",
    phoneNumber: "",

    snackAlert: false,
  }),
};
</script>
