<template>
    <div class="input-field col s12 single-select">
        <select v-model="selected" ref="singleSelect">
            <option
                    :value="default_option.id"
                    selected
                    :data-icon="default_option.img ? require('../../assets/img/' + default_option.img) : ''"
            >{{default_option.name}}</option>
            <option
                    v-for="option in options"
                    :key="option.id"
                    :value="option.id"
                    :data-icon="option.img ? require('../../assets/img/' + option.img) : ''"
            >{{option.name}}</option>
        </select>
        <label>{{label}}</label>
    </div>
</template>

<script>
    export default {
        name: "SingleSelect",
        data: () => ({
            selected: 0,
            singleSelect: null
        }),
        props: {
            options: {
                type: Array,
                default: () => []
            },
            default_option: {
                type: Object,
                default: () => {}
            },
            label: {
                type: String,
                default: () => ''
            }
        },
        watch: {
            selected() {
                this.$emit('selectedOption' ,this.selected)
            }
        },
        mounted() {
            this.singleSelect = window.M.FormSelect.init(this.$refs.singleSelect)
        },
        beforeDestroy() {
            if(this.singleSelect && this.singleSelect.destroy) {
                this.singleSelect.destroy()
            }
        }
    }
</script>

<style lang="scss">

</style>