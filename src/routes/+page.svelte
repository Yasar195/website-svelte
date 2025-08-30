<script>
    import Navigation from "../components/navigation/navigation.svelte";
    import Chat from "../components/chat/chat.svelte";
    import Intro from "../components/intro/intro.svelte";
</script>

<div class="p-4 bg-primary w-full h-screen relative">
    <div class="h-1/6 flex items-center justify-center">
        <Navigation/>
    </div>
    <Intro/>
    <div class="absolute bottom-10 right-10">
        <Chat/>
    </div>
</div>
