<script lang="ts">
  import Button, { Label } from "@smui/button";
  import Card, {
    ActionButtons,
    ActionIcons,
    Actions,
    Content,
  } from "@smui/card";
  import IconButton from "@smui/icon-button";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let damage = 0;
  export let active;
  export let health;
  export let healthBuff = 0;
  export let flip = false;

  let money = 0;

  function endTurn() {
    dispatch("endTurn");
    reset();
  }

  function reset() {
    healthBuff = 0;
    money = 0;
    damage = 0;
  }
</script>

<div class="card-container" class:flip={flip} class:active>
  <Card>
    <Content>
      <div class="mdc-typography--headline3">
        {health}
      </div>
      <div class="mdc-typography--body1">
        <sub>
          {active ? healthBuff > 0 ? `+ ${healthBuff}` : '...' : damage > 0 ? `- ${damage}` : '...'} 
        </sub>
      </div>
    </Content>
    <Actions>
      <ActionButtons>
        <Button disabled={!active} on:click={endTurn}>
          <Label>Done</Label>
        </Button>
        <Button disabled={!active} on:click={reset}>
          <Label>Oops</Label>
        </Button>
      </ActionButtons>
      <ActionIcons>
        <IconButton
          class="material-icons"
          disabled={!active}
          on:click={() => healthBuff++}
        >
          health_and_safety
        </IconButton>
        {active ? healthBuff : 0}
        <IconButton
          class="material-icons"
          disabled={!active}
          on:click={() => money++}
        >
          paid
        </IconButton>
        {money}
        <IconButton
          class="material-icons"
          disabled={!active}
          on:click={() => damage++}
        >
          data_saver_on
        </IconButton>
        {active ? damage : 0}
      </ActionIcons>
    </Actions>
  </Card>
</div>

<style>
  div.card-container {
    opacity: .75;
    background-color: honeydew;
  }

  div.flip {
    transform: rotate(180deg);
  }
  div.active {
    opacity: .85;
  }
</style>
