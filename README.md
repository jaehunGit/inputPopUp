import React, { useState, useRef, useEffect } from "react";
import { useSelector, useDispatch, shallowEqual } from "react-redux";
import {
  Descriptions,
  Select,
  Input,
  message,
  Modal,
  Form,
  Button,
} from "antd";
import { isEmpty } from "lodash";

const InputPopUp = (props) => {
  const { handleClose, setBranch } = props;

  const handleChange = (e) => {
    setBranch(e.target.value);
  };

  return (
    <>
      <Descriptions
        className="table-normal tac"
        layout="vertical"
        column={{ xxl: 4, xl: 4, lg: 4, md: 4, sm: 2, xs: 1 }}
        size="small"
        bordered
      >
        <Descriptions.Item label="분과 분류 추가">
          <Form.Item label="분과 분류명">
            <Input onChange={handleChange} />
          </Form.Item>
        </Descriptions.Item>
      </Descriptions>
      <div className="btn-area" style={{ marginBottom: "15px" }}>
        <Button className="btn-default" onClick={handleClose}>
          닫기
        </Button>
        {/* props.isEditable === true 일 경우만 */}
        {
          <Button className="btn-default type-a" onClick={handleClose}>
            저장
          </Button>
        }
      </div>
    </>
  );
};

export default InputPopUp;
