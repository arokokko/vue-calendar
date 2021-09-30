<template>
    <div class="panel no-margin" :class="[event.type]">
        <div class="panel-heading event-title" >
            {{event.title}}
            <span class="tip" :class="[event.type]">{{event.title}}</span>
        </div>
        
    </div>
</template>

<script>
    export default {
        props: {
            event: {
                type: Object
            },

        },
        
    }
</script>
<style>
    .event-title {
        padding: 0px 5px;
        font-size: 1.5rem;
    }
    .clickable-event {
        text-decoration: underline;
    }
    .panel {
        margin-bottom: 8px;
    }
    .panel-heading {
        white-space: nowrap;
        overflow-x: hidden;
        text-overflow: ellipsis;
        text-decoration: none;
    }
    .tip {
        position: absolute;
        display: none;
        left: 4px;
        z-index: 3;
        background-color: inherit;
        padding: 2px 5px;
        border-radius: 3px;
        margin-top: -23px;
        min-width: 100%;
    }
    .panel-heading:hover .tip {
        display: block;
    }
    
</style>