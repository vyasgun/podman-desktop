<script lang="ts">
import { faTrash } from '@fortawesome/free-solid-svg-icons';
import type { VolumeInfoUI } from './VolumeInfoUI';
import ListItemButtonIcon from '../ui/ListItemButtonIcon.svelte';
import { createEventDispatcher } from 'svelte';

export let volume: VolumeInfoUI;
export let detailed = false;

const dispatch = createEventDispatcher<{ update: VolumeInfoUI }>();

async function removeVolume(): Promise<void> {
  volume.status = 'DELETING';
  dispatch('update', volume);

  await window.removeVolume(volume.engineId, volume.name);
}
</script>

{#if volume.status === 'UNUSED'}
  <ListItemButtonIcon
    title="Delete Volume"
    confirm="{true}"
    onClick="{() => removeVolume()}"
    detailed="{detailed}"
    icon="{faTrash}" />
{/if}
