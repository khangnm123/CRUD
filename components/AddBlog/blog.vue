<template>
    <div>
        <div class="button_context" >
            <b-button v-b-modal.modal-prevent-closing class="btn btn-success" id="three">Create Blog</b-button>
        </div>
        
        <b-modal id="modal-prevent-closing" ref="modal" title="Submit Your Name" @show="resetModal" @hidden="resetModal"
            @ok="handleOk">
            <form ref="form" @submit.stop.prevent="handleSubmit" >
                <b-form-group label="Image" >
                    <b-form-input v-model="blog.image"><img :src="blog.image" alt=""></b-form-input>
                </b-form-group>
                  <b-form-group label="Title" >
                        <b-form-input v-model="blog.title" ></b-form-input>
                    </b-form-group>
                      <b-form-group label="Content" >
                        <b-form-input v-model="blog.content" ></b-form-input>
                    </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        edit: {
            type: Object,
            default: null
        }
    },
    watch: {
        edit() {
            if (this.edit) {
            this.blog = Object.assign({} , this.edit)
            } else {
                this.blog = {
                
            }
           }
        }
    },
    data() {
        return {
            blog: {
                image: "",
                title: "",
                content:""  
            },
            name: '',
            nameState: null,
            submittedNames: []
        }
    },
    
    methods: {
        checkFormValidity() {
            const valid = this.$refs.form.checkValidity()
            this.nameState = valid
            return valid
        },
        resetModal() {
            this.name = ''
            this.nameState = null
        },
        handleOk(bvModalEvent) {
             console.log(this.blog);
            // Prevent modal from closing
            this.$emit("save", this.blog)
            // Prevent modal from closing
            this.blog = {
                image: "",
                title: "",
                 content: ""
            }
            bvModalEvent.preventDefault()
            // Trigger submit handler
            this.handleSubmit()
            
        },
        handleSubmit() {
            // Exit when the form isn't valid
            if (!this.checkFormValidity()) {
                return
            }
            // Push the name to submitted names
            this.submittedNames.push(this.name)
            // Hide the modal manually
            this.$nextTick(() => {
                this.$bvModal.hide('modal-prevent-closing')
            })
        }
    }
}
</script>
<style>
    #three{
        position: relative;
    float: right;
    left: 110px;
    top: 76px;
    }
</style>