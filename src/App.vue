<template>
  <div class="container">
    <div class="output">
      <span style="text-transform: capitalize;">{{output}}</span>
      <img v-if="outputImg" :src="outputImg" width="45">
    </div>

    <br>

    <label>Category: </label>
    <select name="category" id="category" @change="categorySelect">
      <option value="number">Number</option>
      <option value="color">Color</option>
      <option value="woodtype">Wood Type</option>
    </select>

    <br>

    <div v-if="category === 'number'" class="numberInputs">
      <div>
        <label>From: </label>
        <input id="numberFrom" type="number" min="0" value="0" />
      </div>
      <div>
        <label>To: </label>
        <input id="numberTo" type="number" min="0" value="64" />
      </div>
    </div>
    <div v-else style="height: 52px"></div>

    <br>

    <div class="rollBtn" @click="roll">
      <span style="margin-top: -4px">Roll</span>
      <img src="/roll.png" style="margin-top: 8px; margin-right: -10px; margin-left: 5px" width="35" height="35">
    </div>

    <br>

    <div class="footer">
      Developed by T6
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { 
      category: 'number',
      output: "",
      outputImg: ""
    }
  },
  methods: {
    categorySelect() {
      this.category = document.getElementById("category").value;
    },
    roll() {
      if (this.category === 'number') {
        this.outputImg = null;

        const numberFrom = Math.ceil(document.getElementById("numberFrom").value);
        const numberTo = Math.floor(document.getElementById("numberTo").value);

        if (numberTo < numberFrom || numberTo < 0 || numberFrom < 0) {
          this.output = "range error"
        }
        else {
          this.output = Math.floor(Math.random() * (numberTo - numberFrom + 1)) + numberFrom;
        }
      }
      else if (this.category === 'color') {
        const colorOptions = ["black", "red", "green", "brown", "blue", "purple", "cyan", "light_gray", "gray", "pink", "lime", "yellow", "light_blue", "magenta", "orange", "white"]
        const idx = Math.floor(Math.random() * colorOptions.length);

        this.output = colorOptions[idx].replace("_", " ");
        this.outputImg = `colors/${colorOptions[idx]}_dye.png`;
      }
      else if (this.category === 'woodtype') {
        this.outputImg = null;

        const woodOptions = ["oak", "spruce", "birch", "jungle", "acacia", "dark_oak", "mangrove", "cherry", "crimson", "warped"]
        const idx = Math.floor(Math.random() * woodOptions.length);

        this.outputImg = `woodtypes/${woodOptions[idx]}_planks.png`;
        
        if (woodOptions[idx].includes("crimson") || woodOptions[idx].includes("warped")) {
          this.output = woodOptions[idx].replace("_", " ") + " Hyphae";
        }
        else {
          this.output = woodOptions[idx].replace("_", " ") + " Wood";
        }
      }
    }
  },
  mounted() {
    this.roll();
  }
}
</script>

<style>
  @font-face {
      font-family: "MinecraftRegular";
      src: url("Minecraft.ttf");
      
  }

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    color: white;
  }

  .output {
    font-family: "MinecraftRegular";
    font-size: 48px;
    display: flex;
    flex-direction: column;
    width: 300px;
    height: 200px;
    border: 1px gray solid;
    border-radius: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
    image-rendering: pixelated;
  }

  .numberInputs {
    height: 52px;
  }
  .numberInputs label {
    margin-right: 2px;
  }
  .numberInputs input {
    max-width: 100px;
    float: right;
  }

  .rollBtn {
    display: flex;
    justify-content: center;
    align-content: baseline;
    font-family: "MinecraftRegular";
    color: white;
    font-size: 42px;
    background-color: green;
    width: 150px;
    height: 60px;
    border: 1px gray solid;
    border-radius: 30px;
    text-align: center;
    user-select: none; /* Prevents highlighting */
  }
  .rollBtn:hover {
    cursor: pointer;
    background-color: darkgreen;
  }

  .footer {
    font-size: 16px;
    color: gray;
    padding: 2rem 0;
    border-top: 1px dashed gray;
    text-align: center;
    display: inline-block;
    width: 100%;
  }
</style>
