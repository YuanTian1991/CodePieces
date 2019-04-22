<template>
  <v-content style="font-family: 'Cambria', mono;background-color:white">
    <v-container>
      <v-card>
        <el-input
          placeholder="Search any string here"
          suffix-icon="el-icon-search"
          v-model="filterText"
          @keyup.native="filterTable"
        />
        <el-table
          :data="tableData"
          style="width:100%;color:black"
          stripe
          border
          size="mini"
          height="75vh"
          ref="tableRef"
        >
          <el-table-column
            v-for="(item,index) in myhead[celllinetype]"
            :key="index"
            :prop="item.data"
            :label="item.label"
            :sortable="item.data !== null"
            align="center"
            :width="item.data !== null? '170': ''"
          >
            <template slot-scope="scope">
              {{ scope.row[item.data] }}
            </template>

            <el-table-column
              v-for="(m,n) in item.children"
              :key="n"
              :prop="m.data"
              :label="m.label"
              sortable
              align="center"
              width="200"
            >
              <template slot-scope="scope">
                {{ scope.row[m.data] }}
              </template>
            </el-table-column>
          </el-table-column>
        </el-table>
      </v-card>
    </v-container>
  </v-content>
</template>

<script>
import axios from "axios";

function csvtojson(csv) {
  var lines = csv.split("\n");
  var result = [];
  var headers = lines[0].split(",");
  for (var i = 1; i < lines.length - 1; i++) {
    var obj = {};
    var currentline = lines[i].split(",");
    for (var j = 0; j < headers.length; j++) {
      obj[headers[j]] = currentline[j];
    }
    result.push(obj);
  }
  //return result; //JavaScript object
  return result; //JSON
}

export default {
  asyncData({ req, params }) {
    return axios
      .get(
        "https://raw.githubusercontent.com/YuanTian1991/Scripts/master/" +
          params.celllinetype +
          ".csv"
      )
      .then(res => {
        var tmpdata = csvtojson(res.data);
        return {
          tableData: tmpdata,
          celllinetype: params.celllinetype
        };
      })
      .catch(err => {
        return { data: "" };
      });
  },
  data() {
    return {
      filterText: null,
      celllinetype: "",

      myhead: {
        GNS_cell_lines_unmodified: [
          { data: "Cell.line.ID", label: "Cell line ID" },
          {
            data: null,
            label: "GBM Subtype/class",
            children: [
              {
                data: "Transcriptional.subtype",
                label: "Transcriptional Subtype"
              },
              { data: "Methylation.subclass", label: "Methylation Subclass" }
            ]
          },
          {
            data: null,
            label: "IDH status",
            children: [
              { data: "Wild.type", label: "Wild type" },
              { data: "Mutant", label: "Mutant" }
            ]
          },
          {
            data: null,
            label: "Cell line derivatives",
            children: [
              { data: "GFP.Luc", label: "GFP-Luc" },
              { data: "SOX2.Cherry", label: "SOX2-Cherry" },
              { data: "Other", label: "Other" }
            ]
          },
          { data: "Xenograft", label: "Xenograft" },
          { data: "Request.cell.line", label: "Request cell line" }
        ],

        GNS_cell_lines_derivatives: [
          { data: "Cell.line.ID", label: "Cell line ID" },
          {
            data: null,
            label: "GBM Subtype/class",
            children: [
              {
                data: "Transcriptional.subtype",
                label: "Transcriptional Subtype"
              },
              { data: "Methylation.subclass", label: "Methylation Subclass" }
            ]
          },
          {
            data: null,
            label: "IDH status",
            children: [
              { data: "Wild.type", label: "Wild type" },
              { data: "Mutant", label: "Mutant" }
            ]
          },
          {
            data: null,
            label: "Copy number alterations",
            children: [
              { data: "EGFR", label: "EGFR" },
              { data: "PDGFRα", label: "PDGFRα" },
              { data: "Other", label: "Other" }
            ]
          },
          { data: "Request.cell.line", label: "Request cell line" }
        ],

        NS_cell_lines_unmodified: [
          { data: "Cell.line.ID", label: "Cell line ID" },
          {
            data: null,
            label: "Cell line specification",
            children: [
              {
                data: "Region",
                label: "Region"
              },
              { data: "Age", label: "Age" }
            ]
          },
          { data: "Cell.line.derivatives", label: "Cell line derivatives" },
          { data: "Request.cell.line", label: "Request cell line" }
        ],

        NS_cell_lines_derivatives: [
          { data: "Cell.line.ID", label: "Cell line ID" },
          {
            data: null,
            label: "Cell line specification",
            children: [
              {
                data: "Region",
                label: "Region"
              },
              { data: "Age", label: "Age" }
            ]
          },
          { data: "ICC", label: "ICC" },
          { data: "Xenograft", label: "Xenograft" },
          { data: "Request.cell.line", label: "Request cell line" }
        ]
      },

      tableData: []
    };
  },
  computed: {},
  methods: {
    filterTable() {
      const rows = this.$refs.tableRef.$refs.bodyWrapper.getElementsByClassName(
        "el-table__row"
      );
      for (let row of rows) {
        let cells = row.getElementsByTagName("td");
        for (let cell of cells) {
          let innerText = cell.innerText.toLowerCase();
          let filterText = this.filterText.toLowerCase();
          if (innerText.indexOf(filterText) > -1) {
            row.style.display = "";
            break;
          } else {
            row.style.display = "none";
          }
        }
      }
    }
  }
};
</script>

<style>
</style>