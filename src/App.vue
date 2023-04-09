<template>
  <div class="container">
    <div class="output">
      <span>{{output}}</span>
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
        <input id="numberFrom" type="number" placeholder="0" />
      </div>
      <div>
        <label>To: </label>
        <input id="numberTo" type="number" placeholder="64" />
      </div>
    </div>
    <div v-else style="height: 52px"></div>

    <br>

    <button class="rollBtn" @click="roll">Roll</button>

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
    }
  },
  methods: {
    categorySelect() {
      this.category = document.getElementById("category").value;
    },
    roll() {
      if (this.category === 'number') {
        const numberFrom = document.getElementById("numberFrom").value || 0;
        const numberTo = document.getElementById("numberTo").value || 64;

        if (numberTo < numberFrom) {
          this.output = "range error"
        }
        else {
          this.output = Math.floor(Math.random() * (numberTo - numberFrom + 1)) + numberFrom;
        }
      }
      else if (this.category === 'color') {
        const colorOptions = ["Black", "Red", "Green", "Brown", "Blue", "Purple", "Cyan", "Light Gray", "Gray", "Pink", "Lime", "Yellow", "Light Blue", "Magenta", "Orange", "White"]
        const idx = Math.floor(Math.random() * colorOptions.length);
        this.output = colorOptions[idx];
      }
      else if (this.category === 'woodtype') {
        const woodOptions = ["Oak Wood", "Spruce Wood", "Birch Wood", "Jungle Wood", "Acacia Wood", "Dark Oak Wood", "Mangrove Wood", "Cherry Wood", "Crimson Hyphae", "Warped Hyphae"]
        const idx = Math.floor(Math.random() * woodOptions.length);
        this.output = woodOptions[idx];
      }
    }
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
    width: 300px;
    height: 200px;
    border: 1px gray solid;
    border-radius: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
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
    font-family: "MinecraftRegular";
    font-size: 32px;
    width: 100px;
    height: 40px;
    border: 1px gray solid;
    border-radius: 20px;
  }
  .rollBtn:hover {
    cursor: pointer;
  }

  .footer {
    font-size: 16px;
    padding: 2rem 0;
    border-top: 1px dashed white;
    text-align: center;
    display: inline-block;
    width: 100%;
  }
</style>
