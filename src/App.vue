<template>
    <div id="app">
        <div class="container mx-auto">
            <h1 class="text-center font-black text-4xl my-6">URL Clean Up</h1>
            <p class="my-6">
                Make your URLs beautiful again, with a click of a button! Paste
                your ugly domains into the text area below, click the beautify
                URLs button and hey presto! Your URLs are now beautiful again.
                This beats using excels find and replace feature..
            </p>

            <div class="my-6">
                <div class="mb-6">
                    <h4>Before:</h4>
                    <code
                        >http://www.thisurlisveryuntidy.com/because/of/all/these/slashes</code
                    >
                </div>

                <div class="mb-6">
                    <h4>After:</h4>
                    <code>thisurlisveryuntidy.com</code>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div>
                    <label for="uglydomains">Ugly Domains</label>
                    <textarea
                        class="border rounded w-full p-4 mb-2"
                        placeholder="Enter ugly domain list here:"
                        id="uglyTextArea"
                        rows="8"
                        v-model="utaInput"
                        ref="uta"
                    ></textarea>
                    <button
                        class="bg-blue-600 rounded px-6 py-3 font-bold text-white hover:bg-blue-900"
                        type="button"
                        id="beautify-btn"
                        @click="beautify"
                    >
                        beautify urls
                    </button>
                </div>
                <div>
                    <label for="beautifydomains">Very Clean Domains</label>
                    <textarea
                        class="border rounded w-full p-4 mb-2"
                        id="beautifulTextArea"
                        rows="8"
                        v-model="btaInput"
                        ref="bta"
                    ></textarea>
                    <div class="flex">
                        <button
                            class="bg-blue-600 rounded px-6 py-3 font-bold text-white mr-4 hover:bg-blue-900"
                            type="button"
                            id="copy-btn"
                            @click="copy"
                        >
                            {{ copyButton.text }}
                        </button>
                        <button
                            class="bg-blue-600 rounded px-6 py-3 font-bold text-white hover:bg-blue-900"
                            type="button"
                            id="refresh-btn"
                        >
                            refresh textareas
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <footer
            class="container mx-auto relative inset-x-0 bottom-0 py-6 text-sm pt-24"
        >
            <div class="flex items-center justify-between text-gray-700">
                <span>
                    created by
                    <a
                        href="https://mrpbennett.com/"
                        class="hover:underline text-sm"
                        >mrpbennett</a
                    >
                </span>

                <nav>
                    <a
                        href="https://github.com/mrpbennett"
                        class="hover:underline mr-4"
                        >Github</a
                    >
                    <a
                        href="https://twitter.com/mrpbennett"
                        class="hover:underline"
                        >Twitter</a
                    >
                </nav>
            </div>
        </footer>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                uglyDomains: [],
                beautifulDomains: [],
                regex: /^(?:https?:\/\/)?(?:www\.)?/i,
                // text areas...
                btaInput: null,
                utaInput: null,
                // buttons
                copyButton: {
                    text: 'copy urls',
                    copied: false,
                },
            };
        },
        watch: {
            utaInput: function() {
                return this.$refs.uta.value;
            },
            btaInput: function() {
                return this.$refs.bta.value;
            },
        },
        methods: {
            beautify() {
                if (this.$refs.uta.value) {
                    this.uglyDomains = this.$refs.uta.value.split('\n');
                } else {
                    alert('please paste your domains into the ugly box');
                    this.beautifulDomains.length = 0;
                }
                for (let i = 0; i < this.uglyDomains.length; i++) {
                    const url = this.uglyDomains[i];
                    const urlNoProtocol = url
                        .replace(this.regex, '')
                        .split('/')[0];
                    this.beautifulDomains.push(urlNoProtocol);
                    this.$refs.bta.value = this.beautifulDomains.join('\n');
                }
            },
            copy() {
                this.$refs.bta.select();
                document.execCommand('copy');
                this.toggleCopy();
            },
            refesh() {
                this.uglyDomains[0].reset();
                this.beautifulDomains[0].reset();
            },
            toggleCopy() {
                this.copyButton.copied = !this.copyButton.copied;
                this.copyButton.text = !this.copyButton.copied
                    ? 'copied'
                    : 'copy urls';
            },
        },
    };
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }
    label {
        font-weight: bold;
        margin-bottom: 1rem;
    }
    p {
        font-size: 1.5rem;
    }
</style>
