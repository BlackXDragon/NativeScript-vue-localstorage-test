<template>
    <Page class="page" @loaded="onPageLoaded">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Home"></Label>
        </ActionBar>

        <GridLayout rows="auto, *">
            <TextField hint="Enter your text here..." :text="msg" row="0" />
            <Button text="Save message" @tap="saveMsg" row="1" height="300px" />
        </GridLayout>
    </Page>
</template>

<script>
    let LS = require('nativescript-localstorage')
    let dialogs = require('tns-core-modules/ui/dialogs')
    export default {
        data () {
            return {
                msg: ""
            }
        },
        methods: {
            saveMsg() {
                LS.setItem('message', this.msg);
                setTimeout(() => {
                    dialogs.alert({
                        title: "Alert!",
                        message: "Your message has been saved: "+LS.getItem('message') || 'String not found',
                        okButtonText: "OK"
                    });
                }, 3000);
            },
            onPageLoaded() {
                this.msg = LS.getItem('message') || '';
            }
        }
    };
</script>

<style scoped>
</style>
