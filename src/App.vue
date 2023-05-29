<script setup>
  import Button from './components/Button.vue';
  import Spinner from './components/Spinner.vue';
  import Loading from './components/Loading.vue';
  import Divider from './components/Divider.vue';
  import Menu from './components/Menu.vue';
  import MenuItem from './components/MenuItem.vue';
  import Modal from './components/Modal.vue';
  import Table from './components/Table.vue';
</script>

<template>
  <main>
    <section>
      <h2>Buttons</h2>
      <Divider />
      <h4>Variants</h4>
      <div class="flex">
        <Button variant="default">Default</Button>
        <Button variant="primary">Primary</Button>
        <Button variant="secondary">Secondary</Button>
        <Button variant="warning">Warning</Button>
        <Button variant="danger">Danger</Button>
        <Button variant="muted">Muted</Button>
      </div>
      <h4>Sizes</h4>
      <div class="flex">
        <Button size="small">A small button</Button>
        <Button size="regular">A regular button</Button>
        <Button size="large">A large button</Button>
      </div>
      <div class="flex">
        <Button loading variant="default">Default</Button>
        <Button loading variant="primary">Primary</Button>
        <Button loading variant="secondary">Secondary</Button>
        <Button loading variant="warning">Warning</Button>
        <Button loading variant="danger">Danger</Button>
        <Button loading variant="muted">Muted</Button>
      </div>
      <h4>Disabled</h4>
      <div class="flex">
        <Button disabled variant="default">Default</Button>
        <Button disabled variant="primary">Primary</Button>
        <Button disabled variant="secondary">Secondary</Button>
        <Button disabled variant="warning">Warning</Button>
        <Button disabled variant="danger">Danger</Button>
      </div>
      <h4>Links</h4>
      <div class="grid">
        <Button href="https://google.com" variant="default">Default</Button>
        <Button href="https://google.com" variant="primary">Primary</Button>
        <Button href="https://google.com" variant="secondary">Secondary</Button>
        <Button href="https://google.com" variant="warning">Warning</Button>
        <Button href="https://google.com" variant="danger">Danger</Button>
      </div>
    </section>
    <section>
      <h2>Divider</h2>
      <Divider />
    </section>
    <section>
      <h2>Loaders</h2>
      <Divider />
      <h4>Spinner</h4>
      <Spinner />
      <h4>Loader</h4>
      <Loading />
    </section>
    <section>
      <h2>Menu</h2>
      <Divider />
      <div>
        <Menu v-slot="slotProps">
          <MenuItem @click="">Task 1: Milk the gerbil</MenuItem>
          <MenuItem href="https://google.com">Task 1.5: Make this an anchor</MenuItem>
          <Divider dashed />
          <MenuItem>Taks 2: Something something</MenuItem>
          <!-- <div @click="slotProps.hide">hide menu</div> -->
        </Menu>
      </div>
    </section>
    <section>
      <h2>Modal</h2>
      <Divider />
      <div>
        <Modal>
          <h3>This is an example modal</h3>
          <p>It can display whatever content you like</p>
        </Modal>
      </div>
    </section>
    <section>
      <h2>Table</h2>
      <Divider />
      <div>
        <Table></Table>
      </div>
    </section>
  </main>
</template>

<style scoped>
  :global(body) {
    margin: 0;
    padding: 0;
    height: 100vh;
    width: 100%;
    background-color: #f1f2f3;
  }

  main {
    margin: 0 auto;
    max-width: 960px;
    width: 100%;
    padding-top: 3rem;
    display: flex;
    flex-direction: column;
  }

  section {
    background-color: var(--color-white);
    padding: 1rem 2rem;
    border-radius: 3px;
    margin-bottom: 0.5rem;
  }

  section div {
    margin-bottom: 24px;
  }

  .grid {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(2, 1fr);
  }

  .flex > * + * {
    margin-left: 6px;
  }
</style>
