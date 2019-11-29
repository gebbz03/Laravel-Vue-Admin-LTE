<template>
  <div class="container">
    <div class="row mt-5">
      <div class="col-12">
        <div class="card">
          <div class="card-header">
            <h3 class="card-title">Responsive Hover Table</h3>

            <div class="card-tools">
              <button class="btn btn-success" data-toggle="modal" data-target="#newUserModal">
                Add New
                <i class="fas fa-user-plus"></i>
              </button>
            </div>
          </div>
          <!-- /.card-header -->
          <div class="card-body table-responsive p-0">
            <table class="table table-hover">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>Name</th>
                  <th>Email</th>
                  <th>Type</th>
                  <th>Created At</th>
                  <th>Modify</th>
                </tr>
              </thead>
              <tbody>


                <tr v-for="user in users" :key="user.id">
                  <td> {{user.id}} </td>
                  <td> {{user.name}} </td>
                  <td> {{user.email}} </td>
                  <td> {{user.type}} </td>
                  <td> {{user.created_at}} </td>
                  <td>
                    <a href>
                      <i class="fa fa-edit orange"></i>
                    </a>

                    <a href>
                      <i class="fa fa-trash red"></i>
                    </a>
                  </td>
                </tr>

              </tbody>
            </table>
          </div>
          <!-- /.card-body -->
        </div>
        <!-- /.card -->
      </div>
    </div>

    <!-- Modal -->
    <div
      class="modal fade"
      id="newUserModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="newUserModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="newUserModalLabel">Add New User</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>

          <form @submit.prevent="createUser" @keydown="form.onKeydown($event)">
          <div class="modal-body">

            <div class="form-group">
              <input
                v-model="form.name"
                type="text"
                name="name"
                placeholder="Enter you Name.."
                class="form-control"
                :class="{ 'is-invalid': form.errors.has('name') }"
              />
              <has-error :form="form" field="name"></has-error>
            </div>

            <div class="form-group">
              <input
                v-model="form.email"
                type="email"
                name="email"
                placeholder="Enter you Email.."
                class="form-control"
                :class="{ 'is-invalid': form.errors.has('email') }"
              />
              <has-error :form="form" field="email"></has-error>
            </div>


            <div class="form-group">
              <textarea
                v-model="form.bio"
                name="bio"
                id="bio"
                placeholder="Biography for User(Optional).."
                class="form-control"
                :class="{ 'is-invalid': form.errors.has('bio') }"
              ></textarea>
              <has-error :form="form" field="bio"></has-error>
            </div>


            <div class="form-group">
              <p>Select User Role</p>
              <select
                name="type"
                id="type"
                v-model="form.type"
                class="form-control"
                :class="{ 'is-invalid': form.errors.has('type') }"
              >
                <option value="admin">Admin</option>
                <option value="user">Standard User</option>
                <option value="author">Author</option>
              </select>
              <has-error :form="form" field="type"></has-error>
            </div>



            <div class="form-group">
              <input
                v-model="form.password"
                type="password"
                name="password"
                placeholder="Enter you Password.."
                class="form-control"
                :class="{ 'is-invalid': form.errors.has('password') }"
              />
              <has-error :form="form" field="password"></has-error>
            </div>


          </div>
     


          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="submit" class="btn btn-primary">Create</button>
          </div>

         </form>


        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      
      // Create a new form instance\
      users:{},
      form: new Form({
        name: '',
        email: '',
        password: '',
        type: '',
        bio: '',
        photo: ''
      })
    };
  },

  methods:{
    loadUsers(){
      axios.get("api/user").then(({data}) => (this.users=data.data));
    },
    createUser(){
      this.form.post('api/user');
    }
  },

  created() {
    this.loadUsers();
  }
};
</script>
