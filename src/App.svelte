<script lang="ts">
  import Button from "./components/Button.svelte";
  import Checkbox from "./components/Checkbox.svelte";
  import Input from "./components/Input.svelte";
  import Modal from "./components/Modal.svelte";
  import Row from "./components/Row.svelte";
  import Textarea from "./components/Textarea.svelte";
</script>

<main>
  <Row>
    <Button type="primary">Primary</Button>
    <Button type="secondary">Secondary</Button>
    <Button type="danger">Danger</Button>
    <Button type="text">Text</Button>
  </Row>
  <Row>
    <Button type="primary" disabled>Primary</Button>
    <Button type="secondary" disabled>Secondary</Button>
    <Button type="danger" disabled>Danger</Button>
    <Button type="text" disabled>Text</Button>
  </Row>
  <Row>
    <Input prefix="https://" suffix=".com" />
    <Input placeholder="Input" />
    <Input prefix="http://" suffix=".com" disabled placeholder="Disabled" />
  </Row>
  <Row justifyContent="space-around">
    <Checkbox name="Checkbox" />
    <Checkbox name="Disabled" disabled />
  </Row>
  <Row>
    <Textarea rows={5} />
    <Textarea placeholder="Textarea" />
    <Textarea disabled />
  </Row>
  <Modal />
</main>
