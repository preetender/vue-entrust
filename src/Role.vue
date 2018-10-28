<template>
    <div class="role">
        <slot v-if="has"></slot>
        <slot v-else name="error"></slot>
    </div>
</template>

<script>
export default {
    name: 'role',

    props: {
        name: {
            type: String,
            required: true
        },

        strict: {
            type: Boolean,
            default: false
        }
    },

    data() {
        return {
            roles: ['user', 'admin']
        }
    },

    computed: {
        has() {
            //
            // Verificar simples
            //
            if(this.name.indexOf('|') === -1) {
                if(!this.roles.includes(this.name)) {
                    this.invalid(this.name, false);
                    return false;
                }
                return true;
            }

            let names = this.name.split('|');
            
            //
            // Requer todos os papéis
            //
            if(this.strict) {
                if(names.every(name => this.roles.includes(name))) return true;
                
                this.invalid(names.filter(name => !this.roles.includes(name)), false);
                
                return false;
            }

            if(names.some(name => this.roles.includes(name))) return true;

            this.invalid(names, false);
        }
    },

    methods: {
        invalid(role, exists = false) {
            //
            // Emitir evento de falha
            //
            this.$emit('invalid', {role, exists, strict: this.strict});
        }
    }
}
</script>
