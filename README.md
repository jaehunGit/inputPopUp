import React, { useContext, useState, useEffect, useLayoutEffect } from "react";
import { withRouter, ReactDOM } from "react-router-dom";
import { PageTemplate, Header, Footer } from "components";
import { Button, Modal } from "antd";
import data from "./data";

import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-material.css";

import { AgGridReact } from "ag-grid-react";

const OrgTest1 = (props) => {
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

  const columnDefs = [
    { field: "classification" },
    { field: "title" },
    { field: "board" },
    { field: "departmentHead" },
  ];

  const data1 = [
    { title: "CTO", name: "김진국 담당" },
    { title: "DEVICE", name: "DRAM" },
    { title: "BOARD 위원장", name: "Board 위원장 \n 김신순 담당" },
    { title: "Faciliatator", name: "간사:임찬중TL" },
    {
      title: "분과 분류 1",
      name: "Market",
      hello: "강욱성 담당",
      departmentHead: "김민호 PL",
    },
    {
      title: "분과 분류 2",
      name: "DESIGN",
      hello: "정인철 담당",
      departmentHead: "정인철 담당",
    },
  ];

  const nameData = [
    "총 책임자",
    "분과 대분류",
    "Board 위원장",
    "Faciliatator",
    "분과 분류1",
    "분과 분류2",
    "분과 분류3",
    "분과 분류4",
    "분과 분류5",
    "분과 분류6",
    "분과 분류7",
    "분과 분류8",
    "분과 분류9",
  ];

  const titleData = data[0];

  console.log(titleData);

  let test1 = {
    first: { hi: 1 },
  };

  let obj = nameData.reduce((ac, a) => ({ ..."classification", [a]: ac }), {});
  console.log(obj);

  console.log(Object.keys(test1));

  const result = [
    { classification: nameData[0], title: titleData[0].title },
    { classification: nameData[1], title: titleData[1].title },
    { classification: nameData[2], title: titleData[2].title },
    { classification: nameData[3], title: titleData[3].title },
    {
      classification: nameData[4],
      title: titleData[4].title,
      board: titleData[13].title,
      departmentHead: titleData[14].title,
    },
    {
      classification: nameData[5],
      title: titleData[5].title,
      board: titleData[15].title,
      departmentHead: titleData[16].title,
    },
    {
      classification: nameData[6],
      title: titleData[6].title,
      board: titleData[17].title,
      departmentHead: titleData[18].title,
    },
    {
      classification: nameData[7],
      title: titleData[7].title,
      board: titleData[19].title,
      departmentHead: titleData[20].title,
    },
    {
      classification: nameData[8],
      title: titleData[8].title,
      board: titleData[21].title,
      departmentHead: titleData[22].title,
    },
    {
      classification: nameData[9],
      title: titleData[9].title,
      board: titleData[23].title,
      departmentHead: titleData[24].title,
    },
    {
      classification: nameData[10],
      title: titleData[10].title,
      board: titleData[25].title,
      departmentHead: titleData[26].title,
    },
    {
      classification: nameData[11],
      title: titleData[11].title,
      board: titleData[27].title,
      departmentHead: titleData[28].title,
    },
    {
      classification: nameData[12],
      title: titleData[12].title,
      board: titleData[29].title,
      departmentHead: titleData[30].title,
    },
  ];

  const test = (params) => {
    console.log(params);
  };

  return (
    <PageTemplate header={<Header />} footer={<Footer />}>
      <div className="ag-theme-balham" style={gridStyle}>
        <AgGridReact
          columnDefs={columnDefs} //정의된 컬럼정보
          rowData={result} // 그리드 데이터, json data를 넣어 줘야 한다.(조회)
          rowSelection="multiple"
          onCellDoubleClicked={test}
          rowDragManaged={true}
          animateRows={true}
          defaultColDef={defaultColDef}
        />
      </div>
    </PageTemplate>
  );
};

export default withRouter(OrgTest1);
