<template>
    <div
        style="
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        "
    >
        <dl-button
            label="Align Text"
            @click="jsonEditorEl.format()"
        />
        <dl-switch
            v-model="readonly"
            left-label="read only"
        />
        <div style="height: 200px; width: 500px">
            <dl-select
                v-model="mode"
                :options="['text', 'tree']"
                title="Mode"
            />
        </div>
        <div style="height: 200px; width: 500px">
            <dl-json-editor
                ref="jsonEditorEl"
                v-model="jsonModel"
                :readonly="readonly"
                :mode="mode"
            />
        </div>
        <span>JSON: {{ jsonModel }}</span>

        <dl-button @click="dialogState = !dialogState">
            JsonEditor
        </dl-button>
        <dl-dialog-box
            v-model="dialogState"
            volatile
            :width="700"
        >
            <template #header>
                <dl-dialog-box-header
                    title="JsonEditor"
                    @onClose="dialogState = false"
                />
            </template>
            <template #body>
                <div style="height: 350px">
                    <dl-json-editor v-model="dialogJsonModel" />
                </div>
            </template>
        </dl-dialog-box>
        <span>Dialog JSON: {{ dialogJsonModel }}</span>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue-demi'
import {
    DlJsonEditor,
    DlDialogBox,
    DlDialogBoxHeader,
    DlButton,
    DlSwitch,
    DlSelect
} from '../components'
import { DlJsonEditorModes } from '../components/compound/DlJsonEditor/types'
export default defineComponent({
    components: {
        DlJsonEditor,
        DlDialogBox,
        DlDialogBoxHeader,
        DlButton,
        DlSwitch,
        DlSelect
    },
    setup() {
        const jsonModel = ref('')
        const dialogJsonModel = ref('')
        const dialogState = ref(false)
        const jsonEditorEl = ref(null)
        const readonly = ref(false)
        const mode = ref(DlJsonEditorModes.text)

        return {
            jsonModel,
            dialogState,
            dialogJsonModel,
            jsonEditorEl,
            readonly,
            mode
        }
    }
})
</script>
