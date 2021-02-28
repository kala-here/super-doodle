<template>
  <div>
    <p>valid sets part I count: {{validSetsPartI.length}}</p>
    <p>valid sets part II count: {{validSetsPartII.length}}</p>
  </div>
</template>

<script>
import {passwords} from '@/data/passwords.js';
export default {
  name: 'Day2',
  created(){
    this.validateSet();
  },
  data () {
    return {
      validSetsPartI: [],
      validSetsPartII: [],
      passwords
    }
  },
  methods: {
    validateSet(){
      this.validSetsPartI = [];
      this.validSetsPartII = [];
      // look at policy
      for (const set of this.passwords) {
        const policy = set[0];
        const pw = set[1];
        // from the policy, get char
        const char = policy.slice(policy.length -1);
        // if the char is not present, this is not valid and does not contribute to the valid pw count
        if (pw.indexOf(char) === -1) {
          console.log('this pw does not contain the char: ', set);
          continue;
        } else {
          // get char instance range
          const policyInstanceCounts = policy.slice(0, policy.length -2);
          const countsArray = policyInstanceCounts.split('-');
          const min = parseInt(countsArray[0]);
          const max = parseInt(countsArray[1]);

          const charCount = pw.match(new RegExp(char, "g")).length;
          if (charCount >= min && charCount <= max) {
            this.validSetsPartI.push(set);
          }

          const firstIndex = min - 1;
          const nextIndex = max - 1;
          const firstIsChar = pw[firstIndex] === char;
          if (nextIndex > pw.length) {
            console.log('ONLY LOOK AT FIRST ITEM');
            firstIsChar && this.validSetsPartII.push(set);
            continue;
          }
          const secondIsChar = pw[nextIndex] === char;
          const oneIsChar = (!firstIsChar && secondIsChar) || (firstIsChar && !secondIsChar);
          if (oneIsChar) {
             this.validSetsPartII.push(set);
          } else {
            console.log('this set was not valid as part II', set);
          }
        }
      }
    }
  }
}
</script>
