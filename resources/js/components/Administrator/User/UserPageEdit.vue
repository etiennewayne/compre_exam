<template>
    <div>
        <div class="section">
            <div class="container">
                <div class="columns">
                    <div class="column is-8 is-offset-2">
                        <div class="box">
                            <h1 class="title is-5">ADD/MODIFY USER</h1>
                            <form @submit.prevent="submit">
                                <div class="columns">
                                    <div class="column">
                                        <b-field label="Username"
                                                 :type="this.errors.username ? 'is-danger' : ''"
                                                 :message="this.errors.username ? this.errors.username[0] : ''"
                                                 label-position="on-border">
                                            <b-input type="text" v-model="fields.username" placeholder="Username" required/>
                                        </b-field>
                                    </div>
                                </div>

                                <div class="columns">
                                    <div class="column">
                                        <b-field label="Password"
                                                 :type="this.errors.password ? 'is-danger' : ''"
                                                 :message="this.errors.password ? this.errors.password[0] : ''"
                                                 label-position="on-border">
                                            <b-input type="password" password-reveal v-model="fields.password" placeholder="Password"/>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label="Confirm Password" label-position="on-border">
                                            <b-input type="password" password-reveal v-model="fields.password_confirmation" placeholder="Confirm Password"/>
                                        </b-field>
                                    </div>
                                </div>


                                <div class="columns">
                                    <div class="column">
                                        <b-field label="Lastname"
                                                 :type="this.errors.lname ? 'is-danger' : ''"
                                                 :message="this.errors.lname ? this.errors.lname[0] : ''"
                                                 label-position="on-border">
                                            <b-input type="text" v-model="fields.lname" placeholder="Lastname" required/>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label="Firstname"
                                                 :type="this.errors.fname ? 'is-danger' : ''"
                                                 :message="this.errors.fname ? this.errors.fname[0] : ''"
                                                 label-position="on-border">
                                            <b-input type="text" v-model="fields.fname" placeholder="Firstname" required/>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label="Middlename" label-position="on-border">
                                            <b-input type="text" v-model="fields.mname" placeholder="Middlename" />
                                        </b-field>
                                    </div>
                                </div>

                                <div class="columns">
                                    <div class="column">
                                        <b-field label-position="on-border" label="Sex" expanded>
                                            <b-select v-model="fields.sex" expanded>
                                                <option value="MALE">MALE</option>
                                                <option value="FEMALE">FEMALE</option>
                                            </b-select>
                                        </b-field>
                                    </div>
                                    <div class="column">
                                        <b-field label-position="on-border" label="Role" expanded>
                                            <b-select v-model="fields.role" expanded>
                                                <option value="ADMINISTRATOR">ADMINISTRATOR</option>
                                                <option value="STUDENT">STUDENT</option>
                                            </b-select>
                                        </b-field>
                                    </div>
                                </div><!--cols-->

                                <div class="columns">
                                    <div class="column">
                                        <b-field label-position="on-border" label="Contact No.">
                                            <b-input type="text" v-model="fields.contact_no" placeholder="Contact No."></b-input>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label-position="on-border" label="Email">
                                            <b-input type="email" v-model="fields.email" required placeholder="Email"></b-input>
                                        </b-field>
                                    </div>
                                </div>

                                <div class="columns">
                                    <div class="column">
                                        <b-field label-position="on-border" label="Province">
                                            <b-input type="text" v-model="fields.province" placeholder="Province"></b-input>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label-position="on-border" label="City/Municipality">
                                            <b-input type="text" v-model="fields.city" placeholder="City/Municipality"></b-input>
                                        </b-field>
                                    </div>
                                </div>

                                <div class="columns">
                                    <div class="column">
                                        <b-field label-position="on-border" label="Barangay">
                                            <b-input type="text" v-model="fields.barangay" placeholder="Barangay"></b-input>
                                        </b-field>
                                    </div>

                                    <div class="column">
                                        <b-field label-position="on-border" label="Street">
                                            <b-input type="text" v-model="fields.street" placeholder="Street"></b-input>
                                        </b-field>
                                    </div>
                                </div>

                                <div class="buttons">
                                    <button class="button is-primary">SAVE</button>
                                </div>
                            </form><!--form-->
                        </div> <!--box-->
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        edit: {
            type: String,
            default: ''
        },

        dataPrograms: {
            type: String,
            default: ''
        },

        propLearningModes: {
            type: String,
            default: ''
        }
    },
    data(){
        return {
            fields: {},
            bdate: null,
            errors: {},

            dataJSON: {},

            globalId : 0,

            programs: {},
            learningModes: {},
        }
    },
    methods: {

        submit(){
            axios.put('/panel/user/' + this.globalId, this.fields).then(res=>{
                if(res.data.status === 'updated'){
                    this.$buefy.dialog.alert({
                        title: 'UPDATED!',
                        message: 'User updated successfully.',
                        type: 'is-success',
                        onConfirm: ()=> window.location = '/panel/user'
                    });
                }
            }).catch(err=>{
                if(err.response.status === 422){
                    this.errors = err.response.data.errors;
                    console.log(err.response.data.errors);
                }
            })
        },

        formatDate(){
            let mydate = new Date(Date.parse(this.bdate));
            let realDate = mydate.getFullYear() + "-" + ("0" + (mydate.getMonth() + 1)).slice(-2) + "-"+ ("0" + (mydate.getDate())).slice(-2);
            this.fields.bdate = realDate;
        },

        initData(){

            this.programs = JSON.parse(this.dataPrograms);
            this.learningModes = JSON.parse(this.propLearningModes);

            this.dataJSON = JSON.parse(this.edit);
            this.fields = this.dataJSON;
            this.bdate = new Date(this.dataJSON.bdate);
            this.globalId = this.dataJSON.user_id;
        }
    },

    mounted() {
        this.initData();
    }
}
</script>
