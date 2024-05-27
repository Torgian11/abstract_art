<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12">
            <canvas
              width="800"
              height="600"
              :ref="(el) => (canvas = el)"
            ></canvas>
          </v-col>
          <v-col cols="12">
            <v-form>
              <v-select
                v-model="selectedShapes"
                :items="availableShapes"
                label="Select shapes"
                multiple
              ></v-select>
              <v-slider
                v-model="numShapes"
                label="Number of shapes"
                min="1"
                max="100"
              ></v-slider>
              <v-slider
                v-model="minSize"
                label="Minimum size"
                min="1"
                max="100"
              ></v-slider>
              <v-slider
                v-model="maxSize"
                label="Maximum size"
                min="1"
                max="100"
              ></v-slider>
              <v-btn @click="generateArt">Generate Art</v-btn>
            </v-form>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import { ref } from "vue";

export default {
  setup() {
    const canvas = ref(null);
    const numShapes = ref(50);
    const minSize = ref(10);
    const maxSize = ref(50);
    const availableShapes = ref([
      "circles",
      "squares",
      "lines",
      "triangles",
      "hexagons",
      "octagons",
    ]);
    const selectedShapes = ref([
      "circles",
      "squares",
      "lines",
      "triangles",
      "hexagons",
      "octagons",
    ]);
    const getRandomColor = () => {
      return `rgba(${Math.random() * 255}, ${Math.random() * 255}, ${
        Math.random() * 255
      }, ${Math.random()})`;
    };

    const generateArt = () => {
      const ctx = canvas.value.getContext("2d");
      ctx.clearRect(0, 0, 800, 600);

      for (let i = 0; i < numShapes.value; i++) {
        if (selectedShapes.value.includes("circles")) {
          ctx.beginPath();
          ctx.arc(
            Math.random() * 800,
            Math.random() * 600,
            Math.random() * (maxSize.value - minSize.value) + minSize.value,
            0,
            2 * Math.PI
          );
          ctx.fillStyle = getRandomColor();
          ctx.fill();
        }

        if (selectedShapes.value.includes("squares")) {
          ctx.fillStyle = getRandomColor();
          ctx.fillRect(
            Math.random() * 800,
            Math.random() * 600,
            Math.random() * (maxSize.value - minSize.value) + minSize.value,
            Math.random() * (maxSize.value - minSize.value) + minSize.value
          );
        }

        if (selectedShapes.value.includes("lines")) {
          ctx.beginPath();
          ctx.moveTo(Math.random() * 800, Math.random() * 600);
          ctx.lineTo(Math.random() * 800, Math.random() * 600);
          ctx.strokeStyle = getRandomColor();
          ctx.stroke();
        }

        if (selectedShapes.value.includes("triangles")) {
          ctx.beginPath();
          ctx.moveTo(Math.random() * 800, Math.random() * 600);
          ctx.lineTo(
            Math.random() * 800,
            Math.random() * 600 +
              Math.random() * (maxSize.value - minSize.value) +
              minSize.value
          );
          ctx.lineTo(
            Math.random() * 800 +
              Math.random() * (maxSize.value - minSize.value) +
              minSize.value,
            Math.random() * 600
          );
          ctx.fillStyle = getRandomColor();
          ctx.fill();
        }

        if (selectedShapes.value.includes("hexagons")) {
          ctx.beginPath();
          const x = Math.random() * 800;
          const y = Math.random() * 600;
          const size =
            Math.random() * (maxSize.value - minSize.value) + minSize.value;
          ctx.moveTo(x + size * Math.cos(0), y + size * Math.sin(0));
          for (let j = 1; j <= 6; j++) {
            ctx.lineTo(
              x + size * Math.cos((j * Math.PI) / 3),
              y + size * Math.sin((j * Math.PI) / 3)
            );
          }
          ctx.fillStyle = getRandomColor();
          ctx.fill();
        }

        if (selectedShapes.value.includes("octagons")) {
          ctx.beginPath();
          const x = Math.random() * 800;
          const y = Math.random() * 600;
          const size =
            Math.random() * (maxSize.value - minSize.value) + minSize.value;
          ctx.moveTo(x + size * Math.cos(0), y + size * Math.sin(0));
          for (let j = 1; j <= 8; j++) {
            ctx.lineTo(
              x + size * Math.cos((j * Math.PI) / 4),
              y + size * Math.sin((j * Math.PI) / 4)
            );
          }
          ctx.fillStyle = getRandomColor();
          ctx.fill();
        }
      }
    };

    return {
      canvas,
      numShapes,
      minSize,
      maxSize,
      availableShapes,
      selectedShapes,
      generateArt,
    };
  },
};
</script>
