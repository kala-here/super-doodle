<template>
  <div>
    <p>the product of 2 entries summing to 2020: {{productOf2}}</p>
    <p>the product of 3 entries summing to 2020: {{productOf3}}</p>
  </div>
</template>

<script>
import {expenses} from '@/data/expenseReport.js';
export default {
  name: 'Day1',
  data(){
    return {
      expenses,
      under1010: expenses.filter(n => n < 1010 && n > 0),
      over1009: expenses.filter(n => n > 1009 && n < 2020)
    }
  },
  computed: {
    productOf2(){
      // return the product of the 2 numbers from the expense report that sum up to 2020
      // split the array up to start iterating over them
      // we can safely say that it will be a number under half the sum + a number over half the sum (or 2 equal to half the sum which I didn't need to account for because there was only one set to find and we found it with the below solution);
      for (const smaller of this.under1010) {
        for (const bigger of this.over1009) {
          const sum = smaller + bigger;
          if (sum === 2020) {
            console.log('these two summed up = 2020!', smaller, bigger);
            return smaller * bigger;
          }
        }
      }
    },
    productOf3(){
      // return the product of the 3 numbers from the expense report that sum up to 2020
      // FIRSTunder1010 + SECONDunder1010 + nextLowestOver1009
      let i = 0;
      // iterate over under1010
      for (i; i < this.under1010.length; i++) {
        const first = this.under1010[i];
        // iterate over under1010 again making sure not to go over items we've already touched
        let j = i+1;
        for (j; j < this.under1010.length; j++) {
          const second = this.under1010[j];
          const sum = first + second;
          // iterate over
          for (const over of this.over1009) {
            if (sum + over === 2020) {
              console.log('YAY! The sum of these 3 is 2020:',first, second, over);
              return first * second * over;
            }
          }

          // it's not in the latter half
          for (let k = 0; k < this.under1010.length; k++) {
            // iterate again over the array that contains nums under 1010
            // make sure not to include items that already in the equation
            if (![i, j].includes(k)) {
              const third = this.under1010[k];
              if (sum + third === 2020) {
                console.log('YAY! The sum of these 3 (under half) is 2020:',first, second, third);
                return first * second * third;
              }
            }
          }
        }
      }
    }
  }
}
</script>
