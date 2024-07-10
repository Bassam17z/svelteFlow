<script lang="ts">
  import { writable } from "svelte/store";
  import {
    SvelteFlow,
    Controls,
    Background,
    BackgroundVariant,
    MiniMap,
  } from "@xyflow/svelte";
  import "./app.css";
  import "./styling.css";
  import "@xyflow/svelte/dist/style.css";

  const nodes = writable([
    {
      id: "start",
      type: "input",
      data: { label: "" },
      position: { x: 250, y: -100 },
      className: "svelteflow-node start",
       style:"width: 50px;    height: 50px;    background-color: green;    border-radius: 50%;    display: flex;    align-items: center;    justify-content: center;color: white;"
    },
    {
      id: "1",
      type: "input",
      data: { label: "Visa Application Received" },
      position: { x: 250, y: 0 },
      className: "svelteflow-node",
    },
    {
      id: "2",
      type: "default",
      data: { label: "Verify Document" },
      position: { x: 50, y: 100 },
      className: "svelteflow-node",
    },
    {
      id: "3",
      type: "default",
      data: { label: "Eligibility Check" },
      position: { x: 250, y: 100 },
      className: "svelteflow-node",
    },
    {
      id: "4",
      type: "default",
      data: { label: "Background Check" },
      position: { x: 450, y: 100 },
      className: "svelteflow-node",
    },
    {
      id: "5",
      type: "default",
      data: { label: "Make Decision" },
      position: { x: 250, y: 200 },
      className: "svelteflow-node decision",
    },
    {
      id: "6",
      type: "default",
      data: { label: "Email Applicant" },
      position: { x: 150, y: 300 },
      className: "svelteflow-node",
    },
    {
      id: "7",
      type: "default",
      data: { label: "Close Application" },
      position: { x: 150, y: 400 },
      className: "svelteflow-node",
    },
    {
      id: "8",
      type: "default",
      data: { label: "Book Interview" },
      position: { x: 350, y: 300 },
      className: "svelteflow-node",
    },
    {
      id: "9",
      type: "default",
      data: { label: "Conduct Interview" },
      position: { x: 350, y: 400 },
      className: "svelteflow-node",
    },
    {
      id: "10",
      type: "default",
      data: { label: "Make Final Decision" },
      position: { x: 350, y: 500 },
      className: "svelteflow-node decision",
    },
    {
      id: "11",
      type: "default",
      data: { label: "Email Applicant" },
      position: { x: 350, y: 600 },
      className: "svelteflow-node",
   
    },
    {
      id: "end",
      type: "output",
      data: { label: "" },
      position: { x: 150, y: 700 },
      className: "svelteflow-node end",
      style:"  width: 50px;    height: 50px;    background-color: red;    border-radius: 50%;    display: flex;    align-items: center;    justify-content: center;    color: white;"
    },
  ]);

  const edges = writable([
    {
      id: "start-1",
      source: "start",
      target: "1",
      className: "svelteflow-edge-label",
      
    },
    { id: "1-2", source: "1", target: "2", className: "svelteflow-edge-label" },
    { id: "1-3", source: "1", target: "3", className: "svelteflow-edge-label" },
    { id: "1-4", source: "1", target: "4", className: "svelteflow-edge-label" },
    { id: "2-5", source: "2", target: "5", className: "svelteflow-edge-label" },
    { id: "3-5", source: "3", target: "5", className: "svelteflow-edge-label" },
    { id: "4-5", source: "4", target: "5", className: "svelteflow-edge-label" },
    {
      id: "5-6",
      source: "5",
      target: "6",
      label: "No",
      className: "svelteflow-edge-label",
    },
    {
      id: "5-8",
      source: "5",
      target: "8",
      label: "Yes",
      className: "svelteflow-edge-label",
    },
    { id: "6-7", source: "6", target: "7", className: "svelteflow-edge-label" },
    { id: "8-9", source: "8", target: "9", className: "svelteflow-edge-label" },
    {
      id: "9-10",
      source: "9",
      target: "10",
      className: "svelteflow-edge-label",
    },
    {
      id: "10-11",
      source: "10",
      target: "11",
      label: "Yes",
      className: "svelteflow-edge-label",
    },
    {
      id: "7-end",
      source: "7",
      target: "end",
      className: "svelteflow-edge-label",
    },
    {
      id: "11-end",
      source: "11",
      target: "end",
      className: "svelteflow-edge-label",
    },
    {
      id:"10-7",
      source:"10",
      target:"7",
      label:"no",
      className: "svelteflow-edge-label",
    }
  ]);

  const snapGrid: [number, number] = [20, 20];
</script>

 <style>
  
/* General node styles */
.svelteflow-node {
  padding: 10px !important;
  border-radius: 5px !important;
  border: 1px solid #ccc !important;
  background-color: #fff !important;
  text-align: center !important;
  font-size: 14px !important;
  font-family: Arial, sans-serif !important;
}

/* Decision point node styles */
.svelteflow-node.decision {
  background-color: #f9f9f9 !important;
  border: 1px solid #333 !important;
}

/* Start and end node styles */
.svelteflow-node.start {
  background-color: #e0f7e0 !important;
  border: 2px solid #0f0 !important;
}

.svelteflow-node.end {
  background-color: #f7e0e0 !important;
  border: 2px solid #f00 !important;
}

/* Edge label styles */
.svelteflow-edge-label {
  font-size: 12px !important;
  color: #333 !important;
  background: rgba(255, 255, 255, 0.8) !important;
  padding: 2px 5px !important;
  border-radius: 3px !important;
  border: 1px solid #ccc !important;
  text-align: center !important;
}

</style>

<div id="divCon">
  <SvelteFlow
    {nodes}
    {edges}
    {snapGrid}
    fitView
    on:nodeclick={(event) => console.log("on node click", event.detail.node)}
  >
    <Controls />
    <Background variant={BackgroundVariant.Dots} />
    <MiniMap />
  </SvelteFlow>
</div>
