<script lang="ts">
    import * as Dialog from "$lib/components/ui/dialog/index.js";
    import { Button } from "$lib/components/ui/button";
    import { Input } from "$lib/components/ui/input/index.js";
    import { Label } from "$lib/components/ui/label/index.js";
    import Datepicker from "@/components/ui/datepicker/datepicker.svelte";
    import { type DateValue, getLocalTimeZone } from "@internationalized/date";

    export let onSave: (data: {
        ime_letala: string;
        tip: string;
        registrska_st: string;
        Polet_idPolet: number;
    }) => void;

    
    //let cas_vzleta: DateValue | undefined = undefined;
    //let cas_pristanka: DateValue | undefined = undefined;
    //let Pilot_idPilot = 0;

    let isDialogOpen = false;
    let ime_letala: string;
    let tip: string;
    let registrska_st: string;
    let Polet_idPolet: number;

    async function handleSave() {
      
        const flightData = {
            ime_letala,
            tip,
            registrska_st,
            Polet_idPolet
        };

        onSave(flightData);
        isDialogOpen = false;
    }
</script>

<Dialog.Root bind:open={isDialogOpen}>
    <Dialog.Trigger>
        <Button>
            Dodaj novo letalo
        </Button>
    </Dialog.Trigger>
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
            <Dialog.Title>Novo letalo</Dialog.Title>
            <Dialog.Description>
                Tukaj lahko dodate novo letalo.
            </Dialog.Description>
        </Dialog.Header>
        <div class="grid gap-4 py-4">
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="ime_letala" class="text-right">Ime letala</Label>
                <Input id="ime_letala" class="col-span-3" bind:value={ime_letala} />
            </div>
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="tip" class="text-right">Tip</Label>
                <Input id="tip" class="col-span-3" bind:value={tip} />
            </div>
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="registrska" class="text-right">Registrska številka</Label>
                <Input id="registrska" class="col-span-3" bind:value={registrska_st} />
            </div>
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="id_flight" class="text-right">ID poleta</Label>
                <Input id="id_flight" type="number" class="col-span-3" bind:value={Polet_idPolet} />
            </div>
        </div>
        <Dialog.Footer>
            <Button on:click={handleSave}>Shrani</Button>
        </Dialog.Footer>
    </Dialog.Content>
</Dialog.Root>

