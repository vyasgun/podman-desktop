<script lang="ts">
export let status: string;

interface connectionStatusStyle {
  bgColor: string;
  txtColor: string;
  label: string;
}

const roundIconStyle = 'my-auto w-3 h-3 rounded-full';
const labelStyle = 'my-auto ml-1 font-bold text-[9px]';
const statusesStyle = new Map<string, connectionStatusStyle>([
  [
    'started',
    {
      bgColor: 'bg-green-500',
      txtColor: 'text-green-500',
      label: 'ENABLED',
    },
  ],
  [
    'starting',
    {
      bgColor: 'bg-green-500',
      txtColor: 'text-green-500',
      label: 'ENABLING',
    },
  ],
  [
    'stopped',
    {
      bgColor: 'bg-gray-900',
      txtColor: 'text-gray-900',
      label: 'DISABLED',
    },
  ],
  [
    'stopping',
    {
      bgColor: 'bg-red-500',
      txtColor: 'text-red-500',
      label: 'DISABLING',
    },
  ],
  [
    'failed',
    {
      bgColor: 'bg-red-500',
      txtColor: 'text-red-500',
      label: 'FAILED',
    },
  ],
]);
$: statusStyle = statusesStyle.get(status) || {
  bgColor: 'bg-gray-900',
  txtColor: 'text-gray-900',
  label: status.toUpperCase(),
};
</script>

<div aria-label="Connection Status Icon" class="{roundIconStyle} {statusStyle.bgColor}"></div>
<span aria-label="Connection Status Label" class="{labelStyle} {statusStyle.txtColor}">{statusStyle.label}</span>
