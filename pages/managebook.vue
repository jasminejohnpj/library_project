<template>
  <div class="pa-2">
    <v-card color="#757575" class="card1">
      <v-col cols="2" sm="6">
        <v-list-item three-line>
          <v-list-item-content>
            <div class="mb-18">
              <v-btn fab color="cyan darken-1" elevation="0">
                <v-icon size="large" color="green darken-2" icon="mdi-domain"></v-icon>
              </v-btn>
            </div>
            <v-list-item-title class="headline mb-1 white--text">
              Library Book Management
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-col>
      <!-- <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field> -->
      <v-col>
        <div class="pt-2">
          <v-btn @click="addBookStatus" color="secondary">
            Add A New Book
          </v-btn>
          <!-- <v-btn @click="fetchBookList">Book List</v-btn> -->
        </div>
      </v-col>
      <br><br>
      <v-card>
      <v-data-table
            :headers="headers"
            :items="tableData"
            :items-per-page="10"
            class="elevation-1"
            >
           {{tableData}} 
           <template v-slot:item.action="{ item }">
      <v-icon @click="deleteItem(item)">mdi-delete</v-icon>
    </template>
        </v-data-table>
      </v-card>
      <!-- <div class="card" > 
       
        <v-col
          v-for="book in books"
          :key="book.id"
          cols="12"
          sm="6"
          md="4"
          lg="12"
        >
          <v-card color="#9E9E9E">
            <v-card-title>{{book.bookTitle}}
            </v-card-title>
            <v-card-text>
              <v-card-subtitle> {{ book.author }}</v-card-subtitle>
            </v-card-text>
            <v-btn>View</v-btn>
          </v-card>
        </v-col>
      </div> -->
        <v-snackbar v-model="snackAlert">
          <!-- Snackbar message -->
          Book list fetched successfully.
          <template v-slot:action="{ attrs }">
            <v-btn color="pink" text v-bind="attrs" @click="snackAlert = false">
              Close
            </v-btn>
          </template>
        </v-snackbar>
        <v-form ref="form">
          <v-dialog v-model="dialog" persistent max-width="600px">
            <v-card>
              <v-card-title>
                <span class="text-h5">Book Details</span>
              </v-card-title>
              <v-card>
                <v-card-title>
                  {{ title }}
                </v-card-title>
                <v-card-text>{{ author }}</v-card-text>
              </v-card>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue" text @click="closeDialog">Close</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-form>
      </v-card>
      </div>
    
    
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      newbookname: "",
      bibloId: "",
      categorie: "",
      title: "",
      author: "",
      category: "",
      publisher: "",
      accessionno: "",
      imageFile: false,
      books: [], // Initialize as an empty array to store the fetched books
      snackAlert: false,
      dialog: false,
      headers:[
       {text:'Title', value: 'bookTitle'},
       {text:'Author', value: 'author'},
       {text:'Category', value: 'subjectHeading'},
       {text:'Accession No', value: 'accessionNo'},
      
    ],
      tableData :[]

    };
  },
  mounted(){
    this.fetchBookList();
  },
  methods: {
    addBookStatus() {
      this.$router.push({ name: "addbook" });
    },
    async fetchBookList() {
      try {
  const response = await axios.get(`${process.env.apiUrl}admin/all_books`);
  const bookList = response.data; // Assuming the book data is in the 'data' property of the response

  this.books = bookList.docs; 
  console.log(bookList,"Booklist");
  //console.log(bookList);// Update the 'books' property with fetched data
//  bookList.docs.forEach((e,i)=> {

//   console.log(e,i,e._id)
    
//   }); 
  // Corrected the variable name to 'bookList' (lowercase 'l')
  this.tableData = bookList;
  this.showSnackBar("Book list fetched successfully.");
} catch (error) {
  console.error("Error fetching book list", error);
  this.showSnackBar("Error fetching book list.");
}

      // try {
      //   const response = await axios.get(`${process.env.apiUrl}admin/all_books`);
      //   const bookList = response.docs;
      
      //   this.books = bookList; // Update the 'books' property with fetched data
      //   console.log(booklist);
      //   this.showSnackBar("Book list fetched successfully.");
      // } catch (error) {
      //   console.error("Error fetching book list", error);
      //   this.showSnackBar("Error fetching book list.");
      // }
    },
    showSnackBar(message) {
      this.snackAlert = true;
      setTimeout(() => {
        this.snackAlert = false;
      }, 3000);
    },
    closeDialog() {
      this.dialog = false;
    },
  },
};
</script>

<style>
.mx-auto {
  color: #d9c8c8;
}
.pa-2{
  
  position: relative;
}
.card1{
  height: 150px;
 
}
.pt-2{
  position: absolute;
  right: 50px;
  margin-bottom: 100px;
  padding-bottom: 30px;
}
.background{
    background-image: url('@/components/addbookbg.jpeg');
    background-size: cover;
    
}
.card{
  color: #e0e0e0;
}
</style>