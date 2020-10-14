<template>
  <div id="mynetwork"></div>
</template>

<script>
import { Network, DataSet } from "vis-network/standalone/umd/vis-network.min";
export default {
  name: "landsape",
  data() {
    return {
      network: null,
      nodeMap: [],
      nodeValueMap: null,
      nodes: [],
      edges: [],
      options: {
        edges: {
          width: 1,
          widthConstraint: {
            maximum: 70,
          },
          color: {
            color: "#dcdcdc",
            highlight: "#ff9400",
            hover: "#ff9400",
            inherit: "both",
            opacity: 1.0,
          },
          arrows: {
            middle: { enabled: false, scaleFactor: 1, type: "arrow" },
          },
        },
        nodes: {
          shapeProperties: {
            interpolation: false,
          },
          borderWidth: 5,
          shadow: true,
          widthConstraint: {
            maximum: 70,
          },
          color: {
            border: "#42A85F",
            background: "#42A85F",
            highlight: {
              border: "#ff9400",
              background: "#D2E5FF",
            },
            hover: {
              border: "#ff9400",
              background: "#D2E5FF",
            },
          },
          font: {
            size: 8,
            color: "#424242",
            strokeWidth: 0.2,
            strokeColor: "#424242",
          },
        },
        groups: {
          SkillManagementSystem: {
            size: 40,
            shape: "circularImage",
            image: {
              unselected: "src/assets/skill.svg",
              selected: "/static/images/Beekeeper.svg",
            },
          },
          Agents: {
            size: 30,
            shape: "circularImage",
            image: {
              unselected: "src/assets/skill.svg",
              selected: "/static/images/Beekeeper.svg",
            },
          },
          Skill: {
            size: 20,
            shape: "circularImage",
            image: {
              unselected: "src/assets/skill.svg",
              selected: "/static/images/Beekeeper.svg",
            },
          },
        },

        physics: {
          enabled: true,
          adaptiveTimestep: true,
        },
        layout: {
          hierarchical: {
            direction: "UD",
            sortMethod: "directed",
            nodeSpacing: 100,
            treeSpacing: 200,
            blockShifting: true,
            edgeMinimization: true,
            parentCentralization: false,
          },
        },
        interaction: {
          hover: true,
          selectable: true,
          multiselect: true,
          zoomView: true,
          navigationButtons: true,
          keyboard: true,
        },
      },
      container: "",
    };
  },
  mounted() {
    let json = [
      {
        Id: 1,
        name: "COncor agent",
        active: true,
        skill: [
          {
            Id: 1,
            name: "simple Skill",
            active: true,
          },
          {
            Id: 2,
            name: "simple Skill2",
            active: true,
          },
        ],
      },
      {
        Id: 2,
        name: "Concor agent 2",
        skill: [
          {
            Id: 2,
            name: "simple Skill",
            active: true,
          },
          {
            Id: 1,
            name: "simple Skill2",
            active: true,
          },
          {
            Id: 2,
            name: "simple Skill",
            active: true,
          },
          {
            Id: 1,
            name: "simple Skill2",
            active: true,
          },
        ],
      },
      {
        Id: 3,
        name: "COncor agent3",
        active: true,
        skill: [
          {
            Id: 1,
            name: "simple Skill",
            active: true,
          },
          {
            Id: 2,
            name: "simple Skill2",
            active: true,
          },
          {
            Id: 2,
            name: "simple Skill2",
            active: true,
          },
        ],
      },
    ];
    let idCount = 0;
    this.nodeMap = new Map();
    this.nodeValueMap = new Map();
    this.nodes.push({
      id: idCount,
      label: "Skill Management System",
      group: "SkillManagementSystem",
    });
    this.nodeMap.set("beekeeper", "0");
    this.nodeValueMap.set(idCount, { type: "Beekeeper" });
    this.container = document.getElementById("mynetwork");
    json.forEach((agent) => {
      ++idCount;
      this.nodeMap.set(idCount, idCount.toString());
      this.nodeValueMap.set(idCount, { type: "Agents" });
      if (agent.active) {
        this.nodes.push({
          id: idCount,
          label: agent.name,
          group: "Agents",
        });
      } else {
        this.nodes.push({
          id: idCount,
          label: agent.name,
          group: "Agents",
        });
      }
      this.edges.push({ from: 0, to: idCount });
      let skills = agent.skill;
      let skillid = idCount;
      var timesexecuted = 0;
      skills.forEach((skill) => {
        ++skillid;
        this.nodeMap.set(skillid, idCount.toString());
        this.nodeValueMap.set(skillid, { type: "Skill" });
        if (skill.active) {
          this.nodes.push({
            id: skillid,
            label: skill.name,
            group: "Skill",
          });
        } else {
          this.nodes.push({
            id: skillid,
            label: skill.name,
            group: "Skill",
          });
        }
        this.edges.push({ from: idCount, to: skillid });
        ++timesexecuted;
        if (skills.length == timesexecuted) {
          idCount = skillid;
        }
      });
    });

    var data = {
      nodes: new DataSet(this.nodes),
      edges: new DataSet(this.edges),
    };

    this.network = new Network(this.container, data, this.options);
  },
};
</script>

<style>
#mynetwork {
  position: absolute;
  top: 0px;
  right: 0px;
  bottom: 0px;
  left: 0px;
  background-color: #ffffff;
}
</style>