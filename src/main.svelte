<script lang="ts">
  import { ViamProvider } from "@viamrobotics/svelte-sdk";

  import type { DialConf } from "@viamrobotics/sdk";
  import Status from "./lib/status.svelte";
  import Wrap from "./lib/wrap.svelte";

  let { host, credentials, mId, children } = $props();

  const viamlink = '<p>Open this machine on <a href=https://app.viam.com/machine/'+mId+'>Viam</a><br></p>'

  const dialConfigs: Record<string, DialConf> = $derived({
    xxx: {
      host: host,
      credentials: credentials,
      signalingAddress: "https://app.viam.com:443",
      disableSessions: false,
    },
  });
</script>

<ViamProvider dialConfigs={$state.snapshot(dialConfigs)}>
  <Status name="xxx" display="connection to {host}" />
  {@html viamlink}
  <Wrap partID="xxx" />
  {@render children?.()}
</ViamProvider>

<hr>

V2
