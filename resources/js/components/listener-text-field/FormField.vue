<template>
    <default-field :field="field" :errors="errors">
        <template slot="field">
            <div class="relative flex items-stretch">
                <input
                    class="w-full form-control form-input form-input-bordered"
                    :id="field.attribute"
                    :dusk="field.attribute"
                    v-model="value"
                    v-bind="extraAttributes"
                    :disabled="isReadonly"
                    :list="`${field.attribute}-list`"
                    :value="value"
                />

                <div
                    class="absolute rotating text-80 flex justify-center items-center pin-y pin-r mr-3"
                    v-show="calculating"
                >
                    <svg class="w-4 h-4" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                        <path
                            fill="currentColor"
                            d="M457.373 9.387l-50.095 50.102C365.411 27.211 312.953 8 256 8 123.228 8 14.824 112.338 8.31 243.493 7.971 250.311 13.475 256 20.301 256h10.015c6.352 0 11.647-4.949 11.977-11.293C48.159 131.913 141.389 42 256 42c47.554 0 91.487 15.512 127.02 41.75l-53.615 53.622c-20.1 20.1-5.855 54.628 22.627 54.628H480c17.673 0 32-14.327 32-32V32.015c0-28.475-34.564-42.691-54.627-22.628zM480 160H352L480 32v128zm11.699 96h-10.014c-6.353 0-11.647 4.949-11.977 11.293C463.84 380.203 370.504 470 256 470c-47.525 0-91.468-15.509-127.016-41.757l53.612-53.616c20.099-20.1 5.855-54.627-22.627-54.627H32c-17.673 0-32 14.327-32 32v127.978c0 28.614 34.615 42.641 54.627 22.627l50.092-50.096C146.587 484.788 199.046 504 256 504c132.773 0 241.176-104.338 247.69-235.493.339-6.818-5.165-12.507-11.991-12.507zM32 480V352h128L32 480z"
                            class
                        />
                    </svg>
                </div>

            </div>

            <datalist
                v-if="field.suggestions && field.suggestions.length > 0"
                :id="`${field.attribute}-list`"
            >
                <option v-for="suggestion in field.suggestions" :value="suggestion"/>
            </datalist>
        </template>
    </default-field>
</template>

<script>
    import Listener from "../../mixins/Listener";

    export default {
        mixins: [Listener],

        methods: {
            broadcastHandler(response) {
                this.value = response.data.value;
            }
        }
    };
</script>

<style lang="scss">
    @-webkit-keyframes rotating {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(360deg);
        }
    }

    .rotating {
        animation: rotating 2s linear infinite;
    }
</style>
