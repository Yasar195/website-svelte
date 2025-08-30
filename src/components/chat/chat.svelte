<script lang="ts">
    import { MessageCircle, Send, X } from "@lucide/svelte"; 
    import { tick } from "svelte";

    type Message = {
        text: string;
        sender: "user" | "bot";
    };

    type Response = {
        status: number;
        success: boolean;
        data: {
            reply: string;
        };
        error?: string;
    }

    let showChat = false;
    let message = "";
    let messages: Message[] = [];

    let chatContainer: HTMLDivElement;

    async function sendMessage() {
        if (message.trim() === "") return;
        try {
            messages = [...messages, { text: message, sender: "user" }];
            await tick();
            scrollToBottom();

            const response = await fetch("https://chat.yasararafath.in", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({ message: message })
            });

            if (!response.ok) {
                throw new Error(`API error: ${response.status}`);
            }

            const data: Response = await response.json();

            if (data?.success && data?.data?.reply) {
                messages = [...messages, { text: data.data.reply, sender: "bot" }];
            }
            await tick();
            scrollToBottom();

        } catch(error) {
            console.error("error sending message: ", error)
        }

        message = "";
    }

    function scrollToBottom() {
        if (chatContainer) {
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }
    }
</script>

<div class="w-full">
    {#if showChat}
        <div class="w-80 h-96 bg-white rounded-lg shadow-xl flex flex-col">
            <!-- Header -->
            <div class="flex items-center justify-between p-3">
                <h2 class="text-lg font-semibold">Yasar arafath <span class="text-green-400 text-xs">online</span></h2>
                <button on:click={() => (showChat = false)}>
                    <X />
                </button>
            </div>

            <!-- Messages -->
            <div bind:this={chatContainer} class="flex-1 overflow-y-auto p-3 space-y-2">
                {#each messages as msg}
                    <p class="p-2 rounded-xl text-sm max-w-[70%] {msg.sender === 'user' ? 'bg-blue-500 text-white self-end' : 'bg-gray-100 self-start'}">
                        {msg.text}
                    </p>
                {/each}
            </div>

            <!-- Input -->
            <div class="p-2 border-t border-font-primary gap-2 w-full flex justify-evenly items-center ">
                <input
                    type="text"
                    placeholder="Type a message..."
                    bind:value={message}
                    on:keydown={(e) => e.key === 'Enter' && sendMessage()}
                    class="w-5/6 border-2 border-font-primary rounded-lg outline-none px-3 py-1 text-sm"
                />
                <Send/>
            </div>
        </div>
    {:else}
        <button on:click={() => (showChat = true)} class="p-3 bg-blue-500 text-white rounded-full shadow-lg">
            <MessageCircle />
        </button>
    {/if}
</div>
