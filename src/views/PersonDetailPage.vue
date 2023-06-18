<template>
    <BaseModal
    title="!! Alert !!"
    :show="showDelete"
    okButtonLabel="Cancel"
    cancelButtonLabel="Delete"
    >
    <template v-slot:body>
      <div v-if="!hasTasks">
        <span>Do you really want to delete a person </span>
        <b>{{ person.first + ' ' + person.last }}</b>
        <span> ?</span>
      </div>
      <div v-else>
        <span>You are not allowed to delete a person with assigned tasks!</span>
      </div>
    </template>
  </BaseModal>
    <BasePage title="person detail" :loading="loading">
        <template v-slot:topRight>
            <BaseButton label="Edit" @clicked="$router.push('/personform/' + $route.params.id)"/>
        </template>
        <template v-slot:secondLine>
            <h2>{{ person.first + ' ' + person.last }}</h2>
        </template>
        <template v-slot:thirdLine>
            <BaseButton label="delete" @clicked="showDelete=true"/>
        </template>
    </BasePage>
</template>

<script>
    import db from '../utils/db';
    import BaseModal from '../components/BaseModal.vue';
    import BasePage from '../components/BasePage.vue';
    import BaseButton from '../components/BaseButton.vue';

    export default{
        name: 'PersonDetailPage',
        data(){
            return {
                person:{},
                loading:true,
                showDelete: false
            }
        },
        created (){
            db.get('js4persons/' + this.$route.params.id).then(record => {
                this.person = record
                this.loading = false
            })
        },
        components: {BasePage, BaseButton, BaseModal}
    }
</script>

<style>
</style>