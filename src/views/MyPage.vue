<template>
  <v-container>
      <v-layout row wrap>
          <v-flex xs4>
              <v-btn @click="createContainer(parseInt(containerWidth)/10, parseInt(containerHeight)/10)">Create Container</v-btn>
          </v-flex>
          <v-flex xs4>
              <v-text-field
                label="Container Width" outline
                v-model="containerWidth"
            ></v-text-field>
          </v-flex>
          <v-flex xs4>
              <v-text-field
                label="Container Height" outline
                v-model="containerHeight"
            ></v-text-field>
          </v-flex>
          <v-flex xs4>
              <v-btn @click="addObject()">add Object</v-btn>
          </v-flex>
          <v-flex xs4>
              <v-text-field
                label="Object Width" outline
                v-model="objectWidth"
            ></v-text-field>
          </v-flex>
          <v-flex xs4>
              <v-text-field
                label="Object Height" outline
                v-model="objectHeight"
            ></v-text-field>
          </v-flex>
          <v-flex xs12>
              <span>{{masterObject}}</span>
          </v-flex>
      </v-layout>
        <v-stage :config="stageSize">
            <v-layer>
                <v-rect :config="contentBox"></v-rect>
                <template v-for="(item, i) in masterContainer1" >
                    <v-rect :key="'A' + i" :config="masterContainer1[i]"></v-rect>
                </template>
                <template v-for="(item, index) in masterObject" >
                    <v-rect :key="index" :config="masterObject[index]">
                    </v-rect>
                    <!-- <v-text :key="'B' + index" :config="{x: masterObject[index]text: 'Some text on canvas', fontSize: 15}"/> -->
                </template>
                
            </v-layer>
        </v-stage>
  </v-container>
</template>

<script>
const width = window.innerWidth;
const height = window.innerHeight;

export default {
    data() {
        return{
            title: 'Example vue application',
            containerWidth: null,
            containerHeight: null,
            objectWidth: null,
            objectHeight: null,
            masterObject: [],
            // masterContainer1: [],
            stageSize: {
                width: width,
                height: height
            },
            isDragging: false,
            contentBox: {
                x: 500,
                y: 0,
                width: 400,
                height: 150,
                stroke: "black",
                strokeWidth: 1,
            },
            containerProps: {
                width: 10,
                height: 10,
                stroke: "black",
                strokeWidth: 2,
            },
            x: [],
            y: []
        }
    },
    created() {
        
    },
    computed: {
        masterContainer1() {
            let m = []
            this.y.forEach((a) => {
                this.x.forEach((b) => {
                    let c = {
                    width: 10,
                    height: 10,
                    stroke: "black",
                    strokeWidth: 1,
                    }
                    c.y = a
                    c.x = b
                    m.push(c)
                })
                
            })
            console.log(m)
            return m
        }
    },
    methods: {
        // oncreateContainer(){

        // },
        createContainer(x, y){
            
            for(let i = 0; i < x; i++){
                let x = 10 * i
                this.x.push(x)
            }
            for(let i = 0; i < y; i++){
                let y = 10 * i
                this.y.push(y)
            }
            // console.log(this.x)
            // console.log(this.y)
        },
        handleDragStart() {
        this.isDragging = true;
        },
        handleDragEnd() {
        this.isDragging = false;
        },
        addObject() {
            let obj = {
                x: 0,
                y: 0,
                width: parseInt(this.objectWidth),
                height: parseInt(this.objectHeight),
                length: 50,
                stroke: "black",
                strokeWidth: 1,
                draggable: true,
                fill: this.isDragging ? 'yellow' : 'grey'
            }
            obj.x = this.masterObject.length * 5 + 500
            this.masterObject.push(obj)
            // console.log(this.masterObject.length)
        }
    }
}
</script>
