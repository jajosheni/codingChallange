<template>
  <div>
    <div class="explanation">
      <p>Krijo një repository në <a href="https://github.com/">Github</a>.
      </p>
      <p>Në momentin që ke përfunduar bëj <b>commit & push</b>.</p>
      <p>Pikët do të llogariten në bazë të <b>kohës</b>, <b>saktësisë</b> & <b>kompleksitetit të kohës (Big O)</b>.</p>
      <p>______</p>
      <p>Ekziston një matricë(array) <b>M</b> me <b>2</b> rreshta dhe <b>N</b> kolona. Rreshtat kane indeks <b>0</b> dhe
        <b>1</b>,
        ndërsa kolonat <b>0</b> deri në <b>N-1</b>.</p>
      <p>Çdo qelizë e matricës mund të përmbajë <b>0</b> ose <b>1</b>.</p>

      <p><i><b>Dihet se:</b></i></p>
      <p> • shuma e numrave në rreshtin e sipërm është e barabartë me <b>L</b>.</p>
      <p> • shuma e numrave në rreshtin e poshtëm është e barabartë me <b>P</b>.</p>
      <p> • shuma e numrave në kolonën K është e barabartë me <b>C[K]</b>.</p>
      <p>______</p>
      <p>Në dritaren <b>'Test'</b> ndodhet një <b>JSONArray</b>, në çdo objekt të së cilit jepen <b>L</b>, <b>P</b> dhe
        një matricë <b>C (me N
          kolona)</b>.</p>
      <p>Bazuar në këtë informacion ju duhet të gjeneroni matricën <b>M</b>.</p>
      <p>Këtë matricë duhet ta shtoni në një <b>Array</b> si në shembullin në dritaren <b>'Solution'</b>.</p>
      <p>Nëse kjo matricë nuk ekziston, shtoni <b>'E PAMUNDUR'</b><i>(String)</i> në <b>Array</b>.</p>
      <p>______</p>
      <p> - <b>L</b> dhe <b>P</b> janë <b>integer</b> ndërmjet [0..100000]</p>
      <p> - <b>N</b> është <b>integer</b> ndërmjet [1..100000]</p>
      <p> - çdo element i matricës<i>(array)</i> <b>C</b> është një <b>integer</b> me vlerën <b><i>0, 1 ose 2</i></b>.
      </p>
      <p>______</p>
      <p style="color: gray"><b>Në dritaret e mëposhtme janë dhënë 7 teste dhe në krah 7 zgjidhjet përkatëse.</b></p>
      <b style="color: grey"><i>* Duke klikuar 'Check' mund të kontrolloni rezultatin në Console.</i></b>
    </div>
    <div class="jsons-container">
      <div class="vue-json-editor">
        <h3>Test</h3>
        <vue-json-editor ref='testEditor' v-model="test" mode="code"/>
      </div>
      <div class="vue-json-editor">
        <h3>Solution</h3>
        <vue-json-editor ref='solutionEditor' v-model="solution" mode="code"/>
      </div>
    </div>

    <button class="button" @click="onCheck">Check</button>
  </div>
</template>

<script>
import vueJsonEditor from 'vue-json-editor';

export default {
  name: 'Hackathon',
  data() {
    return {
      test: [
        {
          'L': 3,
          'P': 2,
          'C': [2, 1, 1, 0, 1]
        }, {
          'L': 5,
          'P': 6,
          'C': [2, 1, 2, 2, 2, 2]
        }, {
          'L': 2,
          'P': 2,
          'C': [2, 0, 2, 0]
        }, {
          'L': 2,
          'P': 2,
          'C': [2, 2]
        }, {
          'L': 0,
          'P': 0,
          'C': [0, 0, 0]
        }, {
          'L': 2,
          'P': 3,
          'C': [0, 0, 1, 1, 2]
        }, {
          'L': 5,
          'P': 6,
          'C': [2, 0, 2, 2, 2, 2]
        }
      ],
      solution: [
        [
          [1, 1, 0, 0, 1],
          [1, 0, 1, 0, 0]
        ],
        [
          [1, 0, 1, 1, 1, 1],
          [1, 1, 1, 1, 1, 1]
        ],
        [
          [1, 0, 1, 0],
          [1, 0, 1, 0]
        ],
        [
          [1, 1],
          [1, 1]
        ],
        [
          [0, 0, 0],
          [0, 0, 0]
        ],

        'E PAMUNDUR',
        'E PAMUNDUR'
      ],
    };
  },
  components: {
    vueJsonEditor
  },

  methods: {
    onCheck() {
      try {

        let alertMsg = [];
        if (this.$refs.testEditor._data.error || this.$refs.solutionEditor._data.error) {
          alert('Invalid JSON');
        } else {
          let idx = 0;
          this.solution.forEach(solution => {
            console.log('\nSolution' + (idx + 1));
            if (solution !== 'E PAMUNDUR') {
              solution.forEach(row => console.log(row));
              console.log(
                  'Solution L === Test L: ',
                  this.test[idx]['L'] === solution[0].reduce((a, b) => a + b, 0),
              );

              console.log(
                  'Solution P === Test P: ',
                  this.test[idx]['P'] === solution[1].reduce((a, b) => a + b, 0),
              );
              const column_sums = solution.reduce((a, b) => a.map((x, i) => x + (b[i] || 0)));
              const sums_match = JSON.stringify(this.test[idx]['C']) === JSON.stringify(column_sums);
              console.log('Solution Column Sums === Test Column Sums: ', sums_match,
                  '\nC :', column_sums, '\nC :', this.test[idx]['C']);

              alertMsg.push(
                  (idx + 1) + '. ' + (
                      (
                          this.test[idx]['L'] === solution[0].reduce((a, b) => a + b, 0) &&
                          this.test[idx]['P'] === solution[1].reduce((a, b) => a + b, 0) &&
                          sums_match
                      ) ? 'e sakte' : 'e gabuar')
              );
            } else {
              const txt = this.test[idx]['C'].reduce((a, b) => a + b, 0) === (this.test[idx]['L'] + this.test[idx]['P']);
              alertMsg.push((idx + 1) + '. ' + (txt ? 'e gabuar' : 'e sakte'));
            }
            idx++;
          });
          alert('Per me shume hollesi hapni Console\n\n' +
              alertMsg.join('\n'));
        }
      } catch (e) {
        alert('Gjatesite e JSONArray nuk perputhen');
      }
    }
  }
};
</script>
<style>
.jsons-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.vue-json-editor {
  width: 49.5%;
  text-align: center;
}

.jsoneditor-vue, .ace_editor, .ace_layer, .ace_gutter {
  min-height: 500px;
  text-align: left;
}

.explanation {
  text-align: left;
}

.button {
  background-color: #0088ff;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  margin: 10px 2px 4px;
}
</style>
