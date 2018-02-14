<template>

    <button :input="input" :use-icon="useIcon" :class="classes" @click="click" title="Copy to clipboard">
        <svg v-if="useIcon" class="clopy-svg" aria-hidden="true" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
            <path fill="currentColor" d="M433.941 65.941l-51.882-51.882A48 48 0 0 0 348.118 0H176c-26.51 0-48 21.49-48 48v48H48c-26.51 0-48 21.49-48 48v320c0 26.51 21.49 48 48 48h224c26.51 0 48-21.49 48-48v-48h80c26.51 0 48-21.49 48-48V99.882a48 48 0 0 0-14.059-33.941zM266 464H54a6 6 0 0 1-6-6V150a6 6 0 0 1 6-6h74v224c0 26.51 21.49 48 48 48h96v42a6 6 0 0 1-6 6zm128-96H182a6 6 0 0 1-6-6V54a6 6 0 0 1 6-6h106v88c0 13.255 10.745 24 24 24h88v202a6 6 0 0 1-6 6zm6-256h-64V48h9.632c1.591 0 3.117.632 4.243 1.757l48.368 48.368a6 6 0 0 1 1.757 4.243V112z"></path>
        </svg>
    </button>

</template>

<script>

  export default {
    name: 'clopy',
    props: {
      classes: {
        type: String,
        default: 'clopy-button'
      },
      useIcon: {
        type: Boolean,
        default: true
      },
      input: {
        type: String,
        default: null
      }
    },
    methods: {
      click: function() {
        if (!this.input) {
          throw new Error('Failed to copy selection. No input to select!');
        }

        let input = document.querySelector(this.input);
        if (window.clipboardData) {
          window.clipboardData.setData('Text', input.value);
        }

        // Create a temporary input wich we will make not-hidden to make sure it can be copied.
        // it's placed outside of the view for copying then removed.
        let tempInput = document.createElement("input");
        let text = (input.value !== undefined) ? input.value : input.innerText;
        tempInput.setAttribute('value', text);
        tempInput.setAttribute('type', 'text');
        tempInput.style = {
          position: "absolute",
          left: "-1000px",
          top: "-1000px"
        };

        document.querySelector('body').appendChild(tempInput);
        tempInput.select();
        if (!document.execCommand('copy', false, null)) {
          throw new Error('Failed to copy selection.');
        }

        tempInput.remove();
      }
    }
  };
</script>

<style scoped>

    .clopy-button {
        display: inline-block;
        margin-bottom: 0;
        font-weight: normal;
        text-align: center;
        vertical-align: middle;
        -ms-touch-action: manipulation;
        touch-action: manipulation;
        cursor: pointer;
        background-image: none;
        border: 1px solid transparent;
        white-space: nowrap;
        padding: 6px 12px;
        font-size: 14px;
        line-height: 1.42857143;
        border-radius: 4px;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    .clopy-button:hover {
        color: #333333;
        text-decoration: none;
    }

    .clopy-button:active {
        outline: 0;
        background-image: none;
        -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
        box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
    }

    .clopy-button > svg {
        height: 16px;
    }

</style>
