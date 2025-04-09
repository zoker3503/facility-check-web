// App.js
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

const checkItems = [
  {
    id: 1,
    title: "Main Air 압력 확인",
    description: "압력계 정상 여부 확인 및 지정 범위 내 유지",
    image: "/images/air-pressure-gauge.png", // 기본 이미지
  },
  {
    id: 2,
    title: "냉각수 순환 여부",
    description: "냉각수 펌프 작동 여부 확인",
    image: "/images/water-flow.png", // 기본 이미지
  },
];

export default function App() {
  const [results, setResults] = useState({});
  const [inspector, setInspector] = useState("");
  const [date, setDate] = useState("");

  const handleResultChange = (id, value) => {
    setResults((prev) => ({
      ...prev,
      [id]: value,
    }));
  };

  return (
    <div className="p-4 space-y-4 bg-gray-100 min-h-screen">
      <h1 className="text-xl font-bold text-center">📋 설비 점검표</h1>

      {/* 점검자 정보 */}
      <div className="bg-white p-4 rounded-xl shadow-sm space-y-3">
        <div>
          <Label>점검자</Label>
          <Input
            type="text"
            placeholder="홍길동"
            value={inspector}
            onChange={(e) => setInspector(e.target.value)}
          />
        </div>
        <div>
          <Label>점검일정</Label>
          <Input
            type="date"
            value={date}
            onChange={(e) => setDate(e.target.value)}
          />
        </div>
      </div>

      {/* 점검 항목 */}
      {checkItems.map((item) => (
        <Card key={item.id} className="rounded-2xl shadow-md">
          <CardContent className="p-4 space-y-3">
            <h2 className="text-lg font-semibold">{item.title}</h2>
            <p className="text-sm text-gray-600">{item.description}</p>

            {/* 기본 이미지만 표시 */}
            <img
              src={item.image}
              alt={item.title}
              className="w-full h-48 object-contain rounded-md border"
            />

            {/* OK / NG 선택 */}
            <div className="flex items-center gap-4 mt-3">
              <Label>점검 결과:</Label>
              <Button
                variant={results[item.id] === "OK" ? "default" : "outline"}
                onClick={() => handleResultChange(item.id, "OK")}
              >
                ✅ OK
              </Button>
              <Button
                variant={results[item.id] === "NG" ? "destructive" : "outline"}
                onClick={() => handleResultChange(item.id, "NG")}
              >
                ❌ NG
              </Button>
            </div>
          </CardContent>
        </Card>
      ))}
    </div>
  );
}
