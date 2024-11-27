<template>
   <div>
      <header>
         <p>This is default header</p>
         <slot name="header"> </slot>
      </header>
      <main>
         <slot />
      </main>
   </div>
</template>
