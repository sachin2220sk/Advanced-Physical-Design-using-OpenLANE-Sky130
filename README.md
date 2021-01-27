<h3 align="center"> Advanced Physical Design using OpenLANE Sky130</h3>

![](Images_Day_1/Advanced-Physical-Design-using-OpenLANE_Sky130_1.png)

This GitHub repository will demonstrate the work done in Advanced-Physical-Design-using-OpenLANE-Sky130 workshop which is organized by VLSI System Design also called VSD. The main aim of this workshop is to give hands-on experiences on SoC design planning in OpenLANE flow using Google-SkyWater 130nm process design kit (pdk).


<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="##Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK">Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK</a>
      <ul>
        <li><a href="#skywater-pdk-files">Skywater PDK Files</a></li>
        <li><a href="#invoking-openlane">Invoking OpenLANE</a></li>
        <li><a href="#package-importing">Package Importing</a></li>
        <li><a href="#design-folder">Design Folder</a></li>
        <li><a href="#design-folder-hierarchy">Design Folder Hierarchy</a></li>
        <li><a href="#configuration-files">Configuration Files</a></li>
        <li><a href="#prepare-design">Prepare Design</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
      </li>
    <li>
      <a href="#Day 2 - Good floorplan vs bad floorplan and introduction to library cells">Day 2 - Good floorplan vs bad floorplan and introduction to library cells</a>
      <ul>
        <li><a href="#Floorplan">Floorplan</a></li>
        <li><a href="#View-Floorplan-in-Magic">View Floorplan in Magic</a></li>
        <li><a href="#Placement">Placement</a></li>
        <li><a href="#View-Placement-in-Magic">View Placement in Magic</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 3 - Design library cell using Magic Layout and ngspice characterization">Day 3 - Design library cell using Magic Layout and ngspice characterization</a>
      <ul>
        <li><a href="#Clone-the-git-repo-containing-skywater-spice-model-files-and-copy-the-skywater-tech-file-into-folder">Clone the git repo containing skywater spice model files and copy the skywater tech file into folder</a></li>
        <li><a href="#Viewing the Inverter Standard cell in Magic">Viewing the Inverter Standard cell in Magic</a></li>
        <li><a href="#DRC">DRC</a></li>
        <li><a href="#Extraction to Spice using Magic">Extraction to Spice using Magic</a></li>
        <li><a href="#Spice Simulation">Spice Simulation</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 4 - Pre-layout timing analysis and importance of good clock tree">Day 4 - Pre-layout timing analysis and importance of good clock tree</a>
      <ul>
        <li><a href="#LEF File">LEF File</a></li>
        <li><a href="#PnR Guidelines while making Standard Cell set">PnR Guidelines while making Standard Cell set</a></li>
        <li><a href="#Converging grid definitions to track definitions">Converging grid definitions to track definitions</a></li>
        <li><a href="#Creating Port Definition">Creating Port Definition</a></li>
        <li><a href="#Setting port class and port use attributes">Setting port class and port use attributes</a></li>
        <li><a href="#Creating lef file">Creating lef file</a></li>
        <li><a href="#Including Custom Cells in OpenLANE">Including Custom Cells in OpenLANE</a></li>
        <li><a href="#Fixing Slack Violations">Fixing Slack Violations</a></li>
        <li><a href="#Viewing the Custom Inverter cell in Magic">Viewing the Custom Inverter cell in Magic</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA">Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA</a>
      <ul>
        <li><a href="#Generating Power Distribution Network">Generating Power Distribution Network</a></li>
        <li><a href="#Routing">Routing</a></li>
        <li><a href="#SPEF Extraction">SPEF Extraction</a></li>
      </ul>
      </li>
    
  </ol>
  </details>
      

//<!-- Day 1 Inception of Open Source EDA -->

//<!-- toc -->
## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

## Day 3 - Design library cell using Magic Layout and ngspice characterization

## Day 4 - Pre-layout timing analysis and importance of good clock tree
## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

## Day 3 - Design library cell using Magic Layout and ngspice characterization
## Day 4 - Pre-layout timing analysis and importance of good clock tree
## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

## Day 3 - Design library cell using Magic Layout and ngspice characterization
## Day 4 - Pre-layout timing analysis and importance of good clock tree
## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA
## Day 3 - Design library cell using Magic Layout and ngspice characterization
## Day 4 - Pre-layout timing analysis and importance of good clock tree
## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

