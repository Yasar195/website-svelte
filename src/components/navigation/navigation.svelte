<script>
    import { Linkedin } from "@lucide/svelte";
</script>

<!-- Desktop Header (hidden on mobile) -->
<div class="w-full p-4 flex items-center justify-between hidden md:flex">
    <!-- Logo Section -->
    <div class="w-1/4 flex items-center justify-start">
      <h1 class="tracking-wider font-bold text-font-primary">YASAR ARAFATH</h1>
    </div>
    <!-- Navigation Section -->
    <div class="w-2/4 flex items-center justify-center gap-8">
      <h1 class="hover:text-font-primary transition-colors cursor-pointer">services</h1>
      <h1 class="hover:text-font-primary transition-colors cursor-pointer">about</h1>
      <h1 class="hover:text-font-primary transition-colors cursor-pointer">projects</h1>
    </div>
    <!-- Social Links Section -->
    <div class="w-1/4 flex items-center justify-end">
      <Linkedin class="text-font-primary hover:opacity-80 transition-opacity cursor-pointer"/>
    </div>
  </div>
  
  <!-- Mobile Header (visible only on mobile) -->
  <div class="w-full p-4 flex items-center justify-between md:hidden">
    <!-- Mobile Logo -->
    <div class="flex items-center">
      <h1 class="tracking-wider font-bold text-font-primary text-sm">YASAR ARAFATH</h1>
    </div>
    <!-- Mobile Menu Button -->
    <div class="flex items-center gap-4">
      <Linkedin class="text-font-primary"/>
      <button class="text-font-primary">
        <!-- Hamburger menu icon -->
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
      </button>
    </div>
  </div>