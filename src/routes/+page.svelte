<script lang="ts">
    import { onMount } from "svelte";
    import { supabase } from "#lib/SupabaseClient.js";
    import LoginForms from "#lib/components/SvelteComponents/LoginForms.svelte";

    onMount(async () => {
        const { data, error } = await supabase.auth.getSession();

        if (error) {
            console.error("Gagal", error);
        } else {
            console.log("Berhasil (Supabase)", data);
        }
    });
</script>

<main
class="flex min-h-dvh items-center justify-center p-6"
>
    <LoginForms/>
</main>
