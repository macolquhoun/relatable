<template>
  <span class="btn-group btn-rounded" v-if="!display && remove">
    <button type="button" class="btn btn-danger btn-sm close" @click="removeFromChain(index)">
      <span>&times;</span>
    </button>
    <button type="button" class="btn btn-secondary relation" v-bind:class="{'btn-sm': remove}" @click="handleClick()">
      <span class="relation-label" v-if="pluralise">{{label}}'s</span>
      <span class="relation-label" v-else>{{label}}</span>
    </button>
  </span>
  <span class="btn-group btn-rounded-md" v-else-if="!display && !remove">
    <button type="button" class="btn btn-primary font-weight-bold" v-if="!remove" @click="handleClick()">
      &#43;
    </button>
    <button type="button" class="btn btn-secondary relation" v-bind:class="{'btn-sm': remove}" @click="handleClick()">
      <span class="relation-label" v-if="pluralise">{{label}}'s</span>
      <span class="relation-label" v-else>{{label}}</span>
    </button>
  </span>
  <span v-else="display">
    <span v-if="chain.distance.length > 1 || ( chain.distance.length === 1 && chain.distance[0] !== 0 )">your</span> {{label}}
  </span>
</template>

<script>
 import {getRelationLabel} from '../utils';
 import { mapActions } from 'vuex';
 
 export default {
   props: ['chain', 'remove', 'index', 'display', 'pluralise'],
   computed: {
     label(){
       return getRelationLabel( this.chain );
     }
   },
   methods: {
     ...mapActions([
       'removeFromChain',
       'addToChain'
     ]),
     handleClick(){
       if ( this.display === true ) return;
       if ( !this.remove ){
         this.addToChain(this.chain);
       }
     }
   }
 }
</script>
