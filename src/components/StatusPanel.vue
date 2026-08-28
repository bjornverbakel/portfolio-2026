<template>
  <section
    class="decorative-panel device-subpanel"
    aria-label="Power and battery status"
  >
    <div class="decorative-vent" aria-hidden="true">
      <!-- full size -->
      <span class="full-vent" v-for="index in 6" :key="index"></span>

      <!-- small size -->
      <span class="small-vent" v-for="index in 3" :key="index"></span>
    </div>
    <button class="power-button" type="button" aria-label="Power">
      <span aria-hidden="true"></span>
    </button>
    <div class="battery-indicator" role="img" aria-label="Battery indicator">
      <span class="led led-green" aria-hidden="true"></span>
      <p class="emboss-txt select-none">Bat</p>
    </div>
    <div class="mic-indicator" role="img" aria-label="Microphone indicator">
      <span class="led led-blue" aria-hidden="true"></span>
      <p class="emboss-txt select-none">Mic</p>
    </div>
  </section>
</template>

<style>
.decorative-panel {
  --panel-angle: 45deg;
  order: 3;
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  grid-template-rows: auto 1fr auto;
  gap: 8px 16px;
  flex: 1 1 0;
  min-width: 0;
  margin-bottom: 12px;
  padding: clamp(10px, 1.5vw, 18px);
  border: 2px solid var(--panel-border);
  border-radius: 14px 14px var(--device-radius) 14px;
}
.decorative-vent {
  grid-row: 1 / -1;
  display: flex;
  gap: clamp(4px, 0.8vw, 8px);
}
.decorative-vent span {
  flex: 0 0 clamp(3px, 0.45vw, 5px);
  border: 1px solid #272825;
  border-radius: 999px;
  background: var(--vent-surface);
  box-shadow: var(--vent-shadow);
}
.power-button {
  position: relative;
  grid-column: 2;
  grid-row: 1;
  width: clamp(28px, 3.4vw, 38px);
  aspect-ratio: 1;
  cursor: pointer;
  border: 2px solid #161817;
  border-radius: 50%;
  background: linear-gradient(145deg, #818181, #1c1e1d);
  box-shadow:
    inset 1px 1px #ffffff42,
    inset -2px -2px #2b2c2c,
    1px 2px 3px #00000080;
}
.power-button span {
  position: absolute;
  top: 26%;
  left: 29%;
  width: 42%;
  height: 42%;
  border: 2px solid #aaa79f;
  border-top-color: transparent;
  border-radius: 50%;
}
.power-button span::before {
  content: "";
  position: absolute;
  top: -36%;
  left: calc(50% - 1px);
  width: 2px;
  height: 70%;
  background: #aaa79f;
  box-shadow: 1px 1px #111312;
}
.power-button:active {
  background: linear-gradient(145deg, #1c1e1d, #818181);
  transform: translate(1px, 1px);
}
.battery-indicator {
  grid-column: 2;
  grid-row: 3;
  display: grid;
  justify-items: center;
  gap: 4px;
  margin-right: 8px;
}

.small-vent {
  display: none;
}

@media (max-width: 1100px) {
  .full-vent {
    display: none;
  }
  .small-vent {
    display: block;
  }
}

@media (max-width: 1000px) {
  .decorative-panel {
    order: -1;
    flex: 1 0 100%;
    width: auto;
    max-width: 100%;
    min-height: clamp(56px, 10vw, 72px);
    margin: 0;
    grid-template-columns: repeat(4, auto);
    grid-template-rows: 1fr;
    gap: clamp(10px, 4vw, 20px);
    justify-content: space-between;
    border-radius: var(--device-radius) var(--device-radius) 14px 14px;
  }

  .decorative-vent {
    grid-column: 1;
    grid-row: 1;
    gap: clamp(3px, 1vw, 6px);
  }

  .decorative-vent span {
    flex-basis: clamp(3px, 0.6vw, 5px);
    min-height: clamp(30px, 5vw, 40px);
  }

  .power-button,
  .battery-indicator {
    grid-row: 1;
  }

  .power-button {
    grid-column: 4;
    align-self: start;
  }

  .battery-indicator {
    grid-column: 3;
    align-self: end;
  }

  .decorative-panel {
    grid-column: 2;
    align-self: end;
    display: grid;
    justify-items: center;
    gap: 4px;
    margin-right: 8px;
  }
}

.mic-indicator {
  display: none;
}
</style>
