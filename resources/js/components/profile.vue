<style>
.widget-user-header {
  background-position: center center;
  background-size: cover;
}
.widget-user .widget-user-header {
  padding: 1rem;
  height: 300px;
  border-top-left-radius: 0.25rem;
  border-top-right-radius: 0.25rem;
}
.widget-user .widget-user-image > img {
  width: 150px;
  height: 150px;
  border: 3px solid #ffffff;
  object-fit: cover;
}
</style>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12 mt-3">
        <div class="card card-widget widget-user">
          <!-- Add the bg color to the header using any of the bg-* classes -->
          <div
            class="widget-user-header text-white"
            style="background-image:url('./img/user-cover.jpg')"
          >
            <h3 class="widget-user-username ">{{ form.name }}</h3>
            <h5 class="widget-user-desc">{{ form.type }}</h5>
          </div>
          <div class="widget-user-image">
            <img
              class="img-circle"
              :src="getProfilePhoto()"
              alt="User Avatar"
            >
          </div>
          <div class="card-footer">
            <div class="row">
              <div class="col-sm-4 border-right">
                <div class="description-block">
                  <h5 class="description-header">3,200</h5>
                  <span class="description-text">SALES</span>
                </div>
                <!-- /.description-block -->
              </div>
              <!-- /.col -->
              <div class="col-sm-4 border-right">
                <div class="description-block">
                  <h5 class="description-header">13,000</h5>
                  <span class="description-text">FOLLOWERS</span>
                </div>
                <!-- /.description-block -->
              </div>
              <!-- /.col -->
              <div class="col-sm-4">
                <div class="description-block">
                  <h5 class="description-header">35</h5>
                  <span class="description-text">PRODUCTS</span>
                </div>
                <!-- /.description-block -->
              </div>
              <!-- /.col -->
            </div>
            <!-- /.row -->
          </div>
        </div>
        <div class="col-md-13">
          <div class="card">
            <div class="card-header p-2">
              <ul class="nav nav-pills">
                <li class="nav-item"><a
                    class="nav-link active"
                    href="#activity"
                    data-toggle="tab"
                  >Activity</a></li>
                <li class="nav-item"><a
                    class="nav-link"
                    href="#settings"
                    data-toggle="tab"
                  >Settings</a></li>
              </ul>
            </div><!-- /.card-header -->
            <div class="card-body">
              <div class="tab-content">
                <div
                  class="tab-pane active"
                  id="activity"
                >

                  <activities></activities>
                </div>
                <!-- /.tab-pane -->

                <div
                  class="tab-pane"
                  id="settings"
                >
                  <form class="form-horizontal">
                    <div class="form-group row">
                      <label
                        for="inputName"
                        class="col-sm-2 col-form-label"
                      >Name</label>
                      <div class="col-sm-12">
                        <input
                          type="name"
                          v-model="form.name"
                          class="form-control"
                          id="inputName"
                          placeholder="Name"
                          required
                        >
                        <span
                          class="invalid-feedback d-block"
                          role="alert"
                          v-if="form.errors.has('name')"
                          v-text="form.errors.get('name')"
                        ></span>
                      </div>
                    </div>
                    <div class="form-group row">
                      <label
                        for="inputEmail"
                        class="col-sm-2 col-form-label"
                      >Email</label>
                      <div class="col-sm-12">
                        <input
                          type="email"
                          v-model="form.email"
                          class="form-control"
                          id="inputEmail"
                          placeholder="Email"
                          required
                        >
                        <span
                          class="invalid-feedback d-block"
                          role="alert"
                          v-if="form.errors.has('email')"
                          v-text="form.errors.get('email')"
                        ></span>
                      </div>
                    </div>
                    <div class="form-group row">
                      <label
                        for="inputExperience"
                        class="col-sm-2 col-form-label"
                      >Experience</label>
                      <div class="col-sm-12">
                        <textarea
                          class="form-control"
                          id="inputExperience"
                          v-model="form.bio"
                          placeholder="Experience"
                        ></textarea>
                        <span
                          class="invalid-feedback d-block"
                          role="alert"
                          v-if="form.errors.has('bio')"
                          v-text="form.errors.get('bio')"
                        ></span>
                      </div>
                    </div>
                    <div class="form-group row">
                      <label
                        for="photo"
                        class="col-sm-2 col-form-label"
                      >Profile Photo</label>
                      <div class="col-sm-12">
                        <input
                          type="file"
                          class="form-input"
                          name="photo"
                          @change="updateProfile"
                        >
                      </div>
                    </div>
                    <div class="form-group row">
                      <label
                        for="password"
                        class="col-sm-12 col-form-label"
                      >Password (leave empty if not changing)
                      </label>
                      <div class="col-sm-5">
                        <input
                          type="password"
                          v-model="form.password"
                          class="form-control"
                          id="password"
                          placeholder="Password"
                          required
                        >
                        <span
                          class="invalid-feedback d-block"
                          role="alert"
                          v-if="form.errors.has('password')"
                          v-text="form.errors.get('password')"
                        ></span>
                      </div>
                    </div>
                    <div class="form-group row">
                      <div class="col-sm-offset-2 col-sm-12">
                        <button
                          type="submit"
                          class="btn btn-success"
                          @click.prevent="updateInfo"
                        >Update</button>
                      </div>
                    </div>
                  </form>
                </div>
                <!-- /.tab-pane -->
              </div>
              <!-- /.tab-content -->
            </div><!-- /.card-body -->
          </div>
          <!-- /.nav-tabs-custom -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: new Form({
        id: "",
        name: "",
        email: "",
        password: "",
        type: "",
        bio: "",
        photo: ""
      })
    };
  },
  mounted() {
    console.log("Component mounted.");
  },

  methods: {
    getProfilePhoto() {
      let photo =
        this.form.photo.length > 200
          ? this.form.photo
          : "img/profile/" + this.form.photo;
      return photo;
    },
    updateInfo() {
      this.$Progress.start();
      if (this.form.password == "") {
        this.form.password = undefined;
      }
      this.form
        .put("api/profile")
        .then(() => {
          this.$Progress.finish();
          swal.fire({
            icon: "success",
            title: "updated",
            text: "Your profile was updated succefully"
          });
        })

        .catch(() => {
          this.$Progress.fail();
        });
    },
    updateProfile(e) {
      //   console.log("uploading");
      let file = e.target.files[0];
      let reader = new FileReader();
      if (file["size"] < 2111775) {
        reader.onloadend = file => {
          this.form.photo = reader.result;
        };
        reader.readAsDataURL(file);
      } else {
        swal.fire({
          icon: "error",
          title: "Oops..",
          text: "You are uploading a large file"
        });
      }
    }
  },

  created() {
    axios.get("api/profile").then(({ data }) => this.form.fill(data));
  }
};
</script>
