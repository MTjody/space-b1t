<script lang="ts">
  import Button,{ Icon,Label } from "@smui/button";
  import Card,{
  ActionButtons,Actions,
  Content
  } from "@smui/card";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let damage = 0;
  export let active;
  export let health;
  export let healthBuff = 0;
  export let flip = false;

  function endTurn() {
    dispatch("endTurn");
    reset();
  }

  function reset() {
    healthBuff = 0;
    damage = 0;
  }
</script>

<div class="card-container" class:flip class:active>
  <Card>
    <Content>
      <div class="mdc-typography--headline1">
        {health}
      </div>
      <div class="mdc-typography--headline4">
        {active
          ? healthBuff > 0
            ? `+ ${healthBuff}`
            : "..."
          : damage > 0
          ? `- ${damage}`
          : "..."}
      </div>
    </Content>
    <Actions>
      <ActionButtons>
        <Button variant="outlined" class="big" disabled={!active} on:click={endTurn}>
          <Label>Done</Label>
        </Button>
        <Button variant="outlined" class="big" disabled={!active} on:click={reset}>
          <Label>Oops</Label>
        </Button>
        <Button class="big heal" disabled={!active} on:click={() => healthBuff++}>
          <Icon class="material-icons">add_moderator</Icon>
          <Label>{active ? healthBuff : 0}</Label>
        </Button>
        <Button class="big dmg" disabled={!active} on:click={() => damage++}>
          <Icon class="material-icons">rocket_launch</Icon>
          <Label>{active ? damage : 0}</Label>
        </Button>
      </ActionButtons>
    </Actions>
  </Card>
</div>

<style>
  div.card-container {
    opacity: 0.7;
    background-color: honeydew;
  }

  * :global(.big) {
    color: #333333;
  }
  * :global(.dmg) {
    font-size: large;
    color: crimson;
  }
  * :global(.heal) {
    font-size: large;
    color: royalblue;
  }
  div.flip {
    transform: rotate(180deg);
  }
  div.active {
    opacity: 0.9;
  }
</style>
