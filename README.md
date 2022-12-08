import React, { useContext, useState, useEffect, useLayoutEffect } from "react";
import { withRouter, ReactDOM } from "react-router-dom";
import { PageTemplate, Header, Footer } from "components";
import { Button, Modal, Select, Tabs } from "antd";
import data from "./data";

import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-material.css";

import { AgGridReact } from "ag-grid-react";

const OrgTest1 = (props) => {
  const [dataRow, setDataRow] = useState([]);
  const [nameData1, setNameData1] = useState([]);

  const [gridStyle, setGridStyle] = useState({
    width: "100%",
    height: "100vh",
  }); // Grid Width, Height

  const defaultColDef = {
    resizable: true,
    sortable: false,
    editable: false,
    filter: true,
    suppressMenu: true, // Column Menu Hide
    flex: 1,
    wrapText: true, // <-- HERE
    autoHeight: true, // <-- & HERE
  };

  const onGridReady = params => {
    console.log("RoadmapMngt onGridReady!!!!");
    params.api.sizeColumnsToFit(); //자동크기설정(헤더컬럼 자동설정)

  };

  const columnDefs = [
    {
      headerName: 'Action (React)',
      pinned: 'left',
      colId: 'action',
      editable: false,
      maxWidth: 150,
    },
    { field: "classification" },
    { field: "title" },
    { field: "board" },
    { field: "departmentHead" },
  ];

  let titleData = data[0];

  const nameData = [
    "총 책임자",
    "분과 대분류",
    "Board 위원장",
    "Faciliatator",
  ];

  useEffect(() => {
    setDataRow( data[0] );
  },[]);

  useEffect( () => {

    let index = 0; 

    for ( var i=0; i<dataRow.length; i++ ) {
      if ( index < dataRow[i].depth ) {
        index = dataRow[i].depth;
      }
    }

    for ( var i=0; i<index-4; i++ ) {
      nameData.push("분과 분류" + (i+1));
    }

    setNameData1(nameData);

  }, [dataRow]);


  let test1 = {
    first: { hi: 1 },
  };

  const testResult = data[0]

  let result = [
    { classification: nameData1[0], title: titleData[0].title, item: titleData[0].item},
    { classification: nameData1[1], title: titleData[1].title, item: titleData[1].item},
    { classification: nameData1[2], title: titleData[2].title },
    { classification: nameData1[3], title: titleData[3].title },
    { classification: nameData1[4], title: titleData[4].title, board: titleData[13].title, departmentHead: titleData[14].title, boardItem: titleData[13].item, departItem: titleData[14].item},
    { classification: nameData1[5], title: titleData[5].title, board: titleData[15].title, departmentHead: titleData[16].title, boardItem: titleData[15].item, departItem: titleData[16].item },
    { classification: nameData1[6], title: titleData[6].title, board: titleData[17].title, departmentHead: titleData[18].title, boardItem: titleData[17].item, departItem: titleData[18].item },
    { classification: nameData1[7], title: titleData[7].title, board: titleData[19].title, departmentHead: titleData[20].title, boardItem: titleData[19].item, departItem: titleData[20].item },
    { classification: nameData1[8], title: titleData[8].title, board: titleData[21].title, departmentHead: titleData[22].title, boardItem: titleData[21].item, departItem: titleData[22].item },
    { classification: nameData1[9], title: titleData[9].title, board: titleData[23].title, departmentHead: titleData[24].title, boardItem: titleData[23].item, departItem: titleData[24].item },
    { classification: nameData1[10], title: titleData[10].title, board: titleData[25].title, departmentHead: titleData[26].title, boardItem: titleData[25].item, departItem: titleData[26].item },
    { classification: nameData1[11], title: titleData[11].title, board: titleData[27].title, departmentHead: titleData[28].title, boardItem: titleData[27].item, departItem: titleData[28].item },
    { classification: nameData1[12], title: titleData[12].title, board: titleData[29].title, departmentHead: titleData[30].title, boardItem: titleData[29].item, departItem: titleData[30].item },
  ];

  const test = (params) => {
    let objInfo = {};
    // Row Data 의 HIERC항목일련번호(hrcItmSeq) 추출
    let rowData = params.data; // row Data

    console.log( rowData);
    
    const filterTest = testResult.filter(function(test) { return test.item !== rowData.item })
    
    console.log( filterTest );
  };

  const keyChange = params => {
    if ( params == "DRAM" ) {
      console.log("dram");
    } else if ( params == "NAND" ) {
      console.log("nand");
    }
  }

  return (
    <PageTemplate header={<Header />} footer={<Footer />}>
      <Tabs defaultActiveKey="DRAM" onChange={keyChange}>
        <Tabs.TabPane tab="DRAM" key="DRAM"></Tabs.TabPane>
        <Tabs.TabPane tab="NAND" key="NAND"></Tabs.TabPane>
      </Tabs>
      <div className="top-type">
        <Select defaultValue="조직도 version 1.0.0" />
      </div>

      <div className="ag-theme-balham ag-roadmap-type" style={gridStyle}>
        <AgGridReact
        onGridReady={onGridReady}
          columnDefs={columnDefs} //정의된 컬럼정보
          rowData={result} // 그리드 데이터, json data를 넣어 줘야 한다.(조회)
          rowSelection="multiple"
          onCellDoubleClicked={test}
          rowDragManaged={true}
          animateRows={true}
          defaultColDef={defaultColDef}
          suppressColumnVirtualisation={true}
        />
      </div>
    </PageTemplate>
  );
};

export default withRouter(OrgTest1);
