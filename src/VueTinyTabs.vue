<template>
    <div :id="id">
        <slot></slot>
    </div>
</template>

<script>
import tinytabs from '@htoniv/tiny-tabs'
export default {
    name: 'VueTinyTabs',
    components: {
      tinytabs
    },
    props: {
        id: {
            type: String,
            required: true
        },
        anchor: {
            type: Boolean,
            default: false,
            required: false
        },
        closable: {
            type: Boolean,
            default: false,
            required: false
        },
        hideTitle: {
            type: Boolean,
            default: false,
            required: false
        },
        sectionClass: {
            type: String,
            default: 'section',
            required: false
        },
        titleClass: {
            type: String,
            default: 'title',
            required: false
        },
        tabsClass: {
            type: String,
            default: 'tabs',
            required: false
        },
        tabClass: {
            type: String,
            default: 'tab',
            required: false
        }
    },
    mounted() {
        let self = this
        tinytabs(document.querySelector("#"+this.id), {
            anchor: this.anchor,
            hideTitle: this.hideTitle,
            closable: this.closable,
            sectionClass: this.sectionClass,
            titleClass: this.titleClass,
            tabsClass: this.tabsClass,
            tabClass: this.tabClass,
            onClose: function (id) {
                self.handleClose(id)
            },
            onBefore: function (id, tab) {
                self.handleOnBefore(id, tab)
            },
            onAfter: function (id, tab) {
                self.handleOnAfter(id, tab)
            }
		})
	},
    methods: {
        handleClose(id) {
            this.$emit('on-close', id)
        },
        handleOnBefore(id, tab) {
            this.$emit('on-before', id, tab)
        },
        handleOnAfter(id, tab) {
            this.$emit('on-after', id, tab)
        }
    },
}
</script>

<style scoped>
.tinytabs .tabs {
	margin-left: 15px;
	display: flex;
	flex-flow: row wrap;
}
.tinytabs .tabs .tab .close {
	padding-left: 5px;
}
.tinytabs .tabs .tab {
	margin: 0 3px 0 0;
	background: #e1e1e1;
	display: block;
	padding: 6px 15px;
	text-decoration: none;
	color: #666;
	font-weight: bold;
	border-radius: 3px 3px 0 0;
}
.tinytabs .section {
	background: #f1f1f1;
	overflow: hidden;
	padding: 15px;
	clear: both;
	border-radius: 3px;
}
.tinytabs .tab.sel {
	background: #f1f1f1;
	color: #333;
	text-shadow: none;
}
</style>