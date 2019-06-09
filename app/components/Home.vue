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
    let applicationSettings = require('application-settings')
    let dialogs = require('tns-core-modules/ui/dialogs')
    export default {
        data () {
            return {
                msg: ""
            }
        },
        methods: {
            saveMsg() {
                applicationSettings.setString('message', this.msg);
                setTimeout(() => {
                    dialogs.alert({
                        title: "Alert!",
                        message: "Your message has been saved: "+applicationSettings.getString('message', 'String not found'),
                        okButtonText: "OK"
                    });
                }, 3000);
            },
            onPageLoaded() {
                this.msg = applicationSettings.getString('message', '');
            }
        }
    };
</script>

<style scoped>
</style>
