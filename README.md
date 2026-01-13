# Component

## 프로젝트 소개 (Introduction)
- **프로젝트 이름**: Component
- **설명**: 버튼, 토글, 테이블 등 기본 UI 컴포넌트
- **목적**: 여러 SI 프로젝트를 진행하면서, 관리자(admin) 페이지는 크게 변화하지 않기 때문에 재사용성을 높히기 위한 컴포넌트입니다.

<br>

## 데모 & 스크린샷 (Demo & Screenshots)
- 실제 컴포넌트 UI를 확인할 수 있는 화면입니다. 

<br>

## 설치 및 실행 방법(Installation)
```bash
git clone https://github.com/gnaak/component
cd component/frontend
npm install 
npm run dev
```

<br>

## 개발환경 & 기술 스택 (Development Env & Tech Stack)
- **필수 환경**
  - Node.js 18+

- **기술 스택**

<table>
  <tr>
    <th>구분</th>
    <th>내용</th>
  </tr>

  <tr>
    <td>Frontend</td>
    <td>
      <img src="https://img.shields.io/badge/React-61DAFB.svg?&style=for-the-badge&logo=React&logoColor=white" /> 
      <img src="https://img.shields.io/badge/JavaScript-F7DF1E.svg?&style=for-the-badge&logo=JavaScript&logoColor=white" alt="JAVASCRIPT" /> 
      <img src="https://img.shields.io/badge/TypeScript-3172C6.svg?&style=for-the-badge&logo=TypeScript&logoColor=white" /> 
      <img src="https://img.shields.io/badge/HTML5-E34F26.svg?&style=for-the-badge&logo=HTML5&logoColor=white" alt="HTML5" /> 
      <img src="https://img.shields.io/badge/CSS3-1572B6.svg?&style=for-the-badge&logo=CSS3&logoColor=white" alt="CSS3" /> 
      <img src="https://img.shields.io/badge/Tailwind_CSS-06B6D4.svg?&style=for-the-badge&logo=TailwindCSS&logoColor=white" /> 
    </td>
  </tr>
</table>

<br>

## 프로젝트 구조 (Project Structure)
```bash
📁 frontend                     
 ├── 📁 public                    
 ├── 📁 src                     
 │    ├── 📁 assets             
 │    ├── 📁 component
 │    │   └── 📁 common       // 컴포넌트 모음
 │    ├── 📁 container       
 │    │   └── 📄 main.tsx     // 컴포넌트 UI를 확인할 수 있는 페이지
 │    ├── 📁 utils/format
 │    │   ├── 📄 date.ts      // 날짜 변환 훅
 │    │   ├── 📄 number.ts    // 숫자 변환 훅
 │    │   └── 📄 time.ts      // 시간 변환 훅 
 │    ├── 📄 App.css        
 │    ├── 📄 App.tsx         
 │    ├── 📄 global.d.ts       
 │    └── 📄 index.css         
 ├── 📄 .gitignore           
 ├── 📄 index.html           
 ├── 📄 tailwind.config.js 
 ├── 📄 tsconfig.app.json   
 ├── 📄 tsconfig.json         
 ├── 📄 tsconfig.node.json   
 └── 📄 vite.config.ts      
```

<br>

## 주요 기능 (Features)

### 버튼 
**개요**

공통으로 사용하는 버튼 컴포넌트입니다.
`variant`, `size`, `icon`, `full width` 여부 등을 props로 제어할 수 있습니다.

---

**Usage**
```tsx
import Button from "@/components/Button";
import { PlusIcon } from "@/icons";

<Button variant="main" size="md">
  확인
</Button>

<Button
  variant="sub2"
  size="sm"
  leftIcon={<PlusIcon />}
>
  추가
</Button>

<Button
  variant="sub1"
  size="lg"
  rightIcon={<PlusIcon />}
  full
>
  전체 버튼
</Button>
```
---

**Props**
| 이름        | 타입                           | 기본값      | 설명              |
| --------- | ---------------------------- | -------- | --------------- |
| children  | `ReactNode`                  | -        | 버튼 내부 콘텐츠       |
| variant   | `"main" \| "sub1" \| "sub2"` | `"main"` | 버튼 스타일 타입       |
| size      | `"sm" \| "md" \| "lg"`       | `"md"`   | 버튼 크기           |
| leftIcon  | `ReactNode`                  | `null`   | 버튼 왼쪽 아이콘       |
| rightIcon | `ReactNode`                  | `null`   | 버튼 오른쪽 아이콘      |
| full      | `boolean`                    | `false`  | 부모 너비 100%      |
| disabled  | `boolean`                    | `false`  | 비활성화 여부         |
| className | `string`                     | `""`     | 추가 Tailwind 클래스 |
| ...props  | `ButtonHTMLAttributes`       | -        | button 기본 속성    |

---

**Variant**

- main: 주요 액션 버튼
- sub1: 보조 액션 버튼
- sub2: 서브 / 덜 강조된 버튼

각 `variant`는 `hover`, `active`, `disabled` 상태를 모두 지원합니다.

---

**Size**
| size | 높이   | 아이콘 크기 |
| ---- | ---- | ------ |
| sm   | 29px | 16px   |
| md   | 36px | 20px   |
| lg   | 44px | 24px   |

---

**Icon Handling**

- `leftIcon`, `rightIcon`은 **ReactElement**만 처리됩니다.
- 내부에서 `cloneElement`를 사용하여 버튼 size에 맞는 `className(w/h)`가 자동으로 병합됩니다.

```tsx
<Button leftIcon={<PlusIcon className="text-white" />} />
```

---

**Notes**

- `disabled`일 경우:
  - 스타일 변경
  - `pointer-events: none` 적용
- `full={true}`:
  - `w-full` 적용
  - 기본은 콘텐츠 너비(`w-max`)

---

### 토글
**개요**

On / Off 상태를 전환하는 토글(스위치) 컴포넌트입니다.
Controlled / Uncontrolled 방식 모두 지원하며, 크기 옵션과 비활성화 상태를 제공합니다.

---

**Usage**
```tsx
import Toggle from "@/components/Toggle";
```
- 기본 사용(Uncontrolled)
```tsx
<Toggle defaultChecked />
```
- Controlled 사용
```tsx
const [enabled, setEnabled] = useState(false);

<Toggle
  checked={enabled}
  onChange={(v) => setEnabled(v)}
/>;
```
- 비활성화
```tsx
<Toggle disabled />
```
- 크기 조절
```tsx
<Toggle size="sm" />
<Toggle size="md" />
<Toggle size="lg" />
```

---

**Props**
| 이름             | 타입                           | 기본값     | 설명                  |
| -------------- | ---------------------------- | ------- | ------------------- |
| checked        | `boolean`                    | -       | Controlled 모드 상태    |
| defaultChecked | `boolean`                    | `false` | Uncontrolled 모드 초기값 |
| onChange       | `(checked: boolean) => void` | -       | 상태 변경 콜백            |
| size           | `"sm" \| "md" \| "lg"`       | `"md"`  | 토글 크기               |
| disabled       | `boolean`                    | `false` | 비활성화 여부             |
| className      | `string`                     | `""`    | 추가 Tailwind 클래스     |


**Controlled vs Uncontrolled**

Uncontrolled
- `defaultChecked` 사용
- 내부 state로 상태 관리
```tsx
<Toggle defaultChecked />
```

Controlled
- `checked` + `onChange` 사용
- 상태는 상위 컴포넌트에서 관리

```tsx
<Toggle checked={value} onChange={setValue} />
```

---

**Size**
| size | 토글 크기   | 원(circle) 크기 |
| ---- | ------- | ------------ |
| sm   | 32 × 16 | 12 × 12      |
| md   | 40 × 20 | 16 × 16      |
| lg   | 48 × 24 | 20 × 20      |

---

**Behavior**
- 클릭 시 `true / false` 전환
- `disabled`일 경우:
  - 클릭 불가
  - opacity 감소
  - `cursor-not-allowed` 적용
- 상태에 따라 배경색 변경
  - `on` → `bg-main`
  - `off` → `bg-gray-300`

---

**Notes**
- `<button type="button">`으로 구현되어 form submit 방지
- 애니메이션은 `transition-colors`, `transition-transform` 사용
- 원(circle)은 `translate-x-full`로 위치 전환

---

### 체크박스

**개요**

사용자의 선택 여부를 나타내는 체크박스 컴포넌트입니다.  
라벨 표시, 크기 조절(sm/md/lg), 비활성화 상태를 지원합니다.

---

#### Usage

```tsx
import Checkbox from "@/components/Checkbox";
```
---
기본 사용
```tsx
const [checked, setChecked] = useState(false);

<Checkbox
  label="동의합니다"
  checked={checked}
  onChange={setChecked}
/>
```
사이즈 조절
```tsx
<Checkbox size="sm" label="Small" />
<Checkbox size="md" label="Medium" />
<Checkbox size="lg" label="Large" />
```
비활성화
```tsx
<Checkbox disabled label="Disabled Checkbox" />
```

---

**Props**
| 이름        | 타입                           | 기본값     | 설명                |
| --------- | ---------------------------- | ------- | ----------------- |
| label     | `string`                     | `""`    | 체크박스 오른쪽에 표시될 텍스트 |
| checked   | `boolean`                    | `false` | 현재 체크 상태          |
| onChange  | `(checked: boolean) => void` | -       | 체크 상태 변경 콜백       |
| disabled  | `boolean`                    | `false` | 비활성화 여부           |
| size      | `"sm" \| "md" \| "lg"`       | `"md"`  | 체크박스 크기           |
| className | `string`                     | `""`    | 추가 Tailwind 클래스   |

---

**Size**
| size | 체크박스 크기 | 텍스트 크기    | 간격      |
| ---- | ------- | --------- | ------- |
| sm   | 12 × 12 | text-xs   | gap-1.5 |
| md   | 16 × 16 | text-sm   | gap-2   |
| lg   | 20 × 20 | text-base | gap-2.5 |

---

**Behavior**
- 클릭 시 `checked` 값이 `true / false`로 토글
- `onChange` 콜백으로 변경된 상태 전달
- `disabled`일 경우:
  - 클릭 불가
  - opacity 감소
  - `cursor-not-allowed` 적용

---

**Notes**
- `<label>`로 감싸져 있어 텍스트 클릭 시에도 체크 가능
- `accent-main`을 사용해 체크 색상 통일
- 상태 관리는 **Controlled** 방식으로 동작

---

### 라디오 버튼
**개요**

여러 옵션 중 **하나만 선택**할 수 있는 라디오 버튼 컴포넌트입니다.  
같은 `name`을 가진 라디오 버튼끼리 그룹으로 동작하며, 크기 옵션과 비활성화 상태를 지원합니다.

---
**Usage**

```tsx
import RadioButton from "@/components/RadioButton";
```

기본 사용 (그룹)
```tsx
const [selected, setSelected] = useState("male");

<RadioButton
  name="gender"
  value="male"
  label="남성"
  checked={selected === "male"}
  onChange={setSelected}
/>

<RadioButton
  name="gender"
  value="female"
  label="여성"
  checked={selected === "female"}
  onChange={setSelected}
/>
```
사이즈 조절
```tsx
<RadioButton size="sm" label="Small" value="sm" />
<RadioButton size="md" label="Medium" value="md" />
<RadioButton size="lg" label="Large" value="lg" />
```
비활성화
```tsx
<RadioButton disabled label="Disabled Option" value="disabled" />
```

---

**Props**
| 이름        | 타입                        | 기본값     | 설명              |
| --------- | ------------------------- | ------- | --------------- |
| label     | `string`                  | `""`    | 라디오 버튼 라벨       |
| name      | `string`                  | -       | 라디오 그룹 이름       |
| value     | `string`                  | -       | 라디오 버튼 값        |
| checked   | `boolean`                 | `false` | 선택 여부           |
| onChange  | `(value: string) => void` | -       | 선택 값 변경 콜백      |
| disabled  | `boolean`                 | `false` | 비활성화 여부         |
| size      | `"sm" \| "md" \| "lg"`    | `"md"`  | 라디오 버튼 크기       |
| className | `string`                  | `""`    | 추가 Tailwind 클래스 |

---

**Size**
| size | 라디오 크기  | 텍스트 크기    | 간격      |
| ---- | ------- | --------- | ------- |
| sm   | 12 × 12 | text-xs   | gap-1.5 |
| md   | 16 × 16 | text-sm   | gap-2   |
| lg   | 20 × 20 | text-base | gap-2.5 |

---
**Behavior**
- 같은 `name`을 가진 라디오 버튼 중 하나만 선택 가능
- 클릭 시 `onChange(value)` 호출
- `disabled`일 경우:
  - 클릭 불가
  - opacity 감소
  - `cursor-not-allowed` 적용

---


**Notes**

- `<label>`로 감싸져 있어 텍스트 클릭 시에도 선택 가능
- `accent-main`으로 선택 색상 통일
- 상태 관리는 **Controlled** 방식으로 동작

---

### SelectBox

**개요**

여러 옵션 중 하나를 선택할 수 있는 커스텀 SelectBox(드롭다운) 컴포넌트입니다.  
외부 클릭 감지로 자동 닫힘을 지원하며, 크기 및 옵션 리스트가 열리는 방향(top/bottom)을 설정할 수 있습니다.

---

**Usage**

```tsx
import SelectBox from "@/components/SelectBox";
```
기본 사용
```tsx
const [selected, setSelected] = useState<number | null>(null);

<SelectBox
  value={selected}
  onChange={setSelected}
  options={[
    { label: "Option 1", value: 1 },
    { label: "Option 2", value: 2 },
  ]}
/>

Placeholder 사용
<SelectBox
  placeholder="선택하세요"
  options={[
    { label: "Apple", value: "apple" },
    { label: "Banana", value: "banana" },
  ]}
/>
```
팝업 위치 변경
```tsx
<SelectBox position="top" />
<SelectBox position="bottom" />
```
크기 조절
```tsx
<SelectBox size="sm" />
<SelectBox size="md" />
<SelectBox size="lg" />
```
비활성화
```tsx
<SelectBox disabled />
```

---

**Props**
| 이름          | 타입                                             | 기본값        | 설명               |
| ----------- | ---------------------------------------------- | ---------- | ---------------- |
| value       | `string \| number \| null`                     | -          | 선택된 값            |
| onChange    | `(value: string \| number) => void`            | -          | 값 변경 콜백          |
| options     | `{ label: string; value: string \| number }[]` | -          | 옵션 목록            |
| placeholder | `string`                                       | `"선택하세요"`  | 값이 없을 때 표시되는 텍스트 |
| size        | `"sm" \| "md" \| "lg"`                         | `"md"`     | SelectBox 크기     |
| position    | `"top" \| "bottom"`                            | `"bottom"` | 옵션 리스트 표시 방향     |
| disabled    | `boolean`                                      | `false`    | 비활성화 여부          |
| className   | `string`                                       | `""`       | 래퍼 커스텀 클래스       |

---

**Size**
| size | Input 높이 | 옵션 높이 | 텍스트 크기    | 화살표 아이콘 |
| ---- | -------- | ----- | --------- | ------- |
| sm   | 32px     | 28px  | text-xs   | 12px    |
| md   | 40px     | 36px  | text-sm   | 16px    |
| lg   | 48px     | 40px  | text-base | 20px    |

---

**Behavior**
- 버튼 클릭 시 옵션 리스트 열림 / 닫힘
- 옵션 선택 시:
  - `onChange(value)` 호출
  - 리스트 자동 닫힘
- 외부 영역 클릭 시 자동 닫힘
- `disabled`일 경우:
  - 클릭 불가
  - opacity 감소
  - `cursor-not-allowed` 적용

---

**Notes**

- 옵션 리스트는 `absolute` + `z-10`으로 표시
- `position`에 따라 위/아래로 렌더링
- 선택된 옵션은 배경색으로 강조 표시
- 화살표 아이콘은 열림 상태에 따라 회전 애니메이션 적용

---

### 인풋 박스
**개요**

텍스트 입력을 위한 공통 InputBox 컴포넌트입니다.  
크기 옵션(sm/md/lg), 상태(success/error), 좌·우 아이콘 및 아이콘 클릭 이벤트를 지원합니다.

---

**Usage**

```tsx
import InputBox from "@/components/InputBox";
```
기본 사용
```tsx
const [value, setValue] = useState("");

<InputBox
  value={value}
  onChange={setValue}
  placeholder="입력하세요"
/>
```
Input 타입 지정
```tsx
<InputBox type="password" placeholder="비밀번호" />
<InputBox type="email" placeholder="이메일" />
<InputBox type="search" placeholder="검색" />
```
크기 조절
```tsx
<InputBox size="sm" />
<InputBox size="md" />
<InputBox size="lg" />
```
상태 표시 (Success / Error)
```tsx
<InputBox success placeholder="성공 상태" />
<InputBox error placeholder="에러 상태" />
```
아이콘 사용
```tsx
import { Search, Eye } from "lucide-react";

<InputBox
  leftIcon={<Search />}
  rightIcon={<Eye />}
  onRightIconClick={() => console.log("icon clicked")}
  placeholder="검색"
/>
```
비활성화
```tsx
<InputBox disabled placeholder="Disabled Input" />
```
---
**Props**
| 이름               | 타입                                                                          | 기본값       | 설명              |
| ---------------- | --------------------------------------------------------------------------- | --------- | --------------- |
| value            | `string`                                                                    | `""`      | 입력된 값           |
| onChange         | `(value: string) => void`                                                   | -         | 값 변경 콜백         |
| placeholder      | `string`                                                                    | `"입력하세요"` | placeholder 텍스트 |
| type             | `"text" \| "password" \| "email" \| "number" \| "tel" \| "url" \| "search"` | `"text"`  | input 타입        |
| size             | `"sm" \| "md" \| "lg"`                                                      | `"md"`    | Input 크기        |
| disabled         | `boolean`                                                                   | `false`   | 비활성화 여부         |
| success          | `boolean`                                                                   | `false`   | 성공 상태           |
| error            | `boolean`                                                                   | `false`   | 에러 상태           |
| leftIcon         | `ReactNode`                                                                 | -         | 왼쪽 아이콘          |
| rightIcon        | `ReactNode`                                                                 | -         | 오른쪽 아이콘         |
| onLeftIconClick  | `() => void`                                                                | -         | 왼쪽 아이콘 클릭 핸들러   |
| onRightIconClick | `() => void`                                                                | -         | 오른쪽 아이콘 클릭 핸들러  |
| className        | `string`                                                                    | `""`      | 래퍼 커스텀 클래스      |

---

**Size**
| size | 높이   | 텍스트 크기    | 아이콘 크기 |
| ---- | ---- | --------- | ------ |
| sm   | 32px | text-xs   | 12px   |
| md   | 40px | text-sm   | 16px   |
| lg   | 48px | text-base | 20px   |

---

**Behavior**
- 포커스 시 테두리 색상 변경 (`border-main`)
- 상태 우선순위:
  - `error` → red
  - `success` → green
  - `focus` → main
- 아이콘 클릭 시:
  - 이벤트 전파 방지
  - 개별 핸들러 실행
- `disabled`일 경우:
  - 입력 불가
  - opacity 감소
  - `cursor-not-allowed` 적용

---

**Notes**
- 래퍼 클릭 시 input에 포커스 부여
- 아이콘은 button 요소로 감싸 접근성 고려
- 배경은 bg-transparent로 유지

---

### 텍스트 에리아

**개요**

여러 줄 텍스트 입력을 위한 공통 Textarea 컴포넌트입니다.  
크기 옵션(sm/md/lg)과 상태(success/error)에 따라 스타일이 자동으로 변경됩니다.

---

**Usage**

```tsx
import TextareaBox from "@/components/TextareaBox";
```
기본 사용
```tsx
const [text, setText] = useState("");

<TextareaBox
  value={text}
  onChange={setText}
  placeholder="내용을 입력하세요"
/>
```
상태 표시 (Success / Error)
```tsx
<TextareaBox success value="작성 완료" />
<TextareaBox error value="오류 발생" />
```
크기 조절
```tsx
<TextareaBox size="sm" />
<TextareaBox size="md" />
<TextareaBox size="lg" />
```
줄 수 지정
```tsx
<TextareaBox rows={5} />
<TextareaBox size="lg" rows={6} />
```
비활성화
```tsx
<TextareaBox disabled />
```

---

**Props**
| 이름          | 타입                        | 기본값           | 설명              |
| ----------- | ------------------------- | ------------- | --------------- |
| value       | `string`                  | `""`          | 입력된 값           |
| onChange    | `(value: string) => void` | -             | 값 변경 콜백         |
| placeholder | `string`                  | `"내용을 입력하세요"` | placeholder 텍스트 |
| size        | `"sm" \| "md" \| "lg"`    | `"md"`        | Textarea 크기     |
| rows        | `number`                  | `3`           | 기본 줄 수          |
| disabled    | `boolean`                 | `false`       | 비활성화 여부         |
| success     | `boolean`                 | `false`       | 성공 상태           |
| error       | `boolean`                 | `false`       | 오류 상태           |
| className   | `string`                  | `""`          | 래퍼 커스텀 클래스      |

---

**Size**
| size | 최소 높이 | 텍스트 크기    | 패딩          |
| ---- | ----- | --------- | ----------- |
| sm   | 72px  | text-xs   | px-2 py-1.5 |
| md   | 96px  | text-sm   | px-3 py-2   |
| lg   | 120px | text-base | px-3 py-3   |

---

**Behavior**
- 포커스 시 테두리 색상 변경 (`border-main`)
- 상태 우선순위:
  - `error` → red
  - `success` → green
  - `focus` → main
- `resize: none`으로 크기 고정
- `disabled`일 경우:
  - 입력 불가
  - opacity 감소
  - `cursor-not-allowed` 적용

---

**Notes**
- 래퍼 클릭 시 textarea에 포커스 적용
- 배경은 `bg-transparent` 유지
- `rows`는 기본 높이에 추가로 반영됨

---

### 모달
**개요**

확인 / 취소용 기본 Modal 컴포넌트입니다.  
제목, 설명, 버튼 구성(0/1/2개)을 유연하게 제어할 수 있으며, ESC 키 및 오버레이 클릭으로 닫기를 지원합니다.

---

**Usage**

```tsx
import Modal from "@/components/Modal";
```
기본 사용
```tsx
const [open, setOpen] = useState(false);

<Modal
  open={open}
  onClose={() => setOpen(false)}
  title="저장하시겠습니까?"
  description="변경 사항이 적용됩니다."
/>
```
버튼 한 개만 사용하는 경우
```tsx
<Modal
  open={open}
  onClose={handleClose}
  title="완료되었습니다."
  buttonCount={1}
  primaryText="확인"
/>
```
버튼 없는 알림
```tsx
<Modal
  open={open}
  onClose={handleClose}
  title="알림"
  buttonCount={0}
/>
```
버튼 텍스트 & 이벤트 커스터마이징
```tsx
<Modal
  open={open}
  onClose={handleClose}
  title="삭제하시겠습니까?"
  description="삭제 후에는 복구할 수 없습니다."
  primaryText="삭제"
  secondaryText="취소"
  onPrimary={handleDelete}
  onSecondary={handleClose}
/>
```
오버레이 클릭 비활성화
```tsx
<Modal closeOnOverlay={false} />
```
크기 조절
```tsx
<Modal size="sm" />
<Modal size="md" />
<Modal size="lg" />
```

--- 

**Props**
| 이름             | 타입                     | 기본값    | 설명           |
| -------------- | ---------------------- | ------ | ------------ |
| open           | `boolean`              | -      | 모달 열림 여부     |
| onClose        | `() => void`           | -      | 모달 닫기 핸들러    |
| title          | `string`               | -      | 모달 제목        |
| description    | `string`               | -      | 설명 텍스트       |
| size           | `"sm" \| "md" \| "lg"` | `"md"` | 모달 크기        |
| buttonCount    | `0 \| 1 \| 2`          | `2`    | 버튼 개수        |
| primaryText    | `string`               | `"확인"` | 기본 버튼 텍스트    |
| secondaryText  | `string`               | `"취소"` | 보조 버튼 텍스트    |
| onPrimary      | `() => void`           | -      | 기본 버튼 클릭 핸들러 |
| onSecondary    | `() => void`           | -      | 보조 버튼 클릭 핸들러 |
| closeOnOverlay | `boolean`              | `true` | 오버레이 클릭 시 닫기 |
| className      | `string`               | `""`   | 모달 컨테이너 클래스  |
| bodyClassName  | `string`               | `""`   | 내용 래퍼 클래스    |

---

**Size**
| size | 최소 / 최대 너비    |
| ---- | ------------- |
| sm   | 224px ~ 256px |
| md   | 256px ~ 320px |
| lg   | 320px ~ 512px |

---

**Behavior**
- `open === false`일 경우 렌더링되지 않음
- ESC 키 입력 시 `onClose` 호출
- 오버레이 클릭 시:
  - `closeOnOverlay=true` → 닫힘
  - `false` → 무시
- 버튼 동작:
  - `onPrimary` / `onSecondary`가 있으면 해당 핸들러 실행
  - 없으면 기본적으로 `onClose` 호출

---

**Notes**
- `fixed` + `z-40`으로 화면 중앙에 표시
- 오버레이는 `bg-black/40` 사용
- 내부 클릭 시 이벤트 전파 차단
- 버튼은 공통 `Button` 컴포넌트 사용

---

### 폼 모달
**개요**

폼 입력이나 복합 컨텐츠를 담기 위한 확장형 Modal 컴포넌트입니다.  
헤더 정렬 방식, 푸터 버튼 구성, 본문 컨텐츠를 유연하게 조합할 수 있습니다.

---

**Usage**

```tsx
import FormModal from "@/components/FormModal";
```
기본 사용
```tsx
<FormModal
  open={open}
  onClose={handleClose}
  title="제목"
>
  내용...
</FormModal>
```
헤더 타입 지정
```tsx
<FormModal headerType="center" title="가운데 정렬" />
<FormModal headerType="left" title="왼쪽 정렬" />
<FormModal headerType="none" showCloseIcon />
```
폼 예제
```tsx
<FormModal
  open={open}
  onClose={handleClose}
  title="사용자 정보"
  footerType={2}
  primaryText="저장"
  secondaryText="취소"
  onPrimary={handleSave}
>
  <InputBox placeholder="이름" />
  <InputBox placeholder="이메일" />
</FormModal>
```
푸터 버튼 구성
```tsx
<FormModal footerType={0} />
<FormModal footerType={1} primaryText="확인" />
<FormModal footerType={2} />
```
푸터 버튼 정렬
```tsx
<FormModal footerAlign="left" />
<FormModal footerAlign="center" />
<FormModal footerAlign="right" />
```
크기 조절
```tsx
<FormModal size="sm" />
<FormModal size="md" />
<FormModal size="lg" />
```
오버레이 클릭 비활성화
```tsx
<FormModal closeOnOverlay={false} />
```
---

**Props**
| 이름             | 타입                              | 기본값        | 설명            |
| -------------- | ------------------------------- | ---------- | ------------- |
| open           | `boolean`                       | -          | 모달 열림 여부      |
| onClose        | `() => void`                    | -          | 모달 닫기 핸들러     |
| headerType     | `"center" \| "left" \| "none"`  | `"center"` | 헤더 타입         |
| title          | `string`                        | -          | 제목 텍스트        |
| description    | `string`                        | -          | 설명 텍스트        |
| children       | `ReactNode`                     | -          | 본문 컨텐츠        |
| size           | `"sm" \| "md" \| "lg"`          | `"md"`     | 모달 크기         |
| footerType     | `0 \| 1 \| 2`                   | `2`        | 푸터 버튼 개수      |
| footerAlign    | `"left" \| "center" \| "right"` | `"right"`  | 푸터 정렬         |
| primaryText    | `string`                        | `"확인"`     | 주 버튼 텍스트      |
| secondaryText  | `string`                        | `"취소"`     | 보조 버튼 텍스트     |
| onPrimary      | `() => void`                    | -          | 주 버튼 클릭 핸들러   |
| onSecondary    | `() => void`                    | -          | 보조 버튼 클릭 핸들러  |
| closeOnOverlay | `boolean`                       | `true`     | 오버레이 클릭 시 닫기  |
| showCloseIcon  | `boolean`                       | `true`     | 우측 상단 X 버튼 표시 |
| className      | `string`                        | `""`       | 모달 컨테이너 클래스   |
| bodyClassName  | `string`                        | `""`       | 바디 영역 클래스     |

---

**Size**
| size | 최대 너비 |
| ---- | ----- |
| sm   | 384px |
| md   | 448px |
| lg   | 512px |

---

**Behavior**
- `open === false`일 경우 렌더링되지 않음
- ESC 키 입력 시 `onClose` 호출
- 오버레이 클릭 시:
  - `closeOnOverlay=true` → 닫힘
  - `false` → 유지
- 헤더:
  - `headerType="none"`이면 title/description 숨김
  - X 버튼은 항상 우측 상단 고정
- 푸터:
  - 버튼 개수(0/1/2) 및 정렬 방식 지정 가능

---

**Notes**

- 내부 클릭 시 이벤트 전파 차단
- Body 영역은 `overflow-auto`로 스크롤 대응
- 버튼은 공통 `Button` 컴포넌트 사용

---

### 테이블
**개요**

데이터 목록을 행(row)과 열(column) 형태로 표시하는 재사용 가능한 Table 컴포넌트입니다.  
컬럼 정의(`columns`)를 기반으로 Header / Body가 자동 구성되며, 커스텀 셀 렌더링과 행 클릭, 줄무늬(striped) 옵션을 지원합니다.

---

**Usage**

```tsx
import Table from "@/components/Table";
```
기본 사용
```tsx
const columns = [
  { key: "name", header: "이름" },
  { key: "age", header: "나이", align: "center" },
];

const data = [
  { name: "홍길동", age: 30 },
  { name: "김철수", age: 25 },
];

<Table columns={columns} data={data} />;
```
컬럼 너비 & 정렬
```tsx
const columns = [
  { key: "name", header: "이름", width: "150px" },
  { key: "price", header: "가격", align: "right" },
];
```
커스텀 셀 렌더링
```tsx
const columns = [
  {
    key: "status",
    header: "상태",
    render: (row) => <StatusTag type={row.status} />,
  },
];
```
행 클릭 이벤트
```tsx
<Table
  columns={columns}
  data={data}
  onRowClick={(row) => console.log(row)}
/>
```
줄무늬 테이블
```tsx
<Table columns={columns} data={data} striped />
```
행 크기 조절
```tsx
<Table size="sm" />
<Table size="md" />
<Table size="lg" />
```

---

**Props**
| 이름         | 타입                     | 기본값     | 설명             |
| ---------- | ---------------------- | ------- | -------------- |
| columns    | `Column[]`             | -       | 테이블 컬럼 정의      |
| data       | `any[]`                | -       | 테이블 데이터        |
| size       | `"sm" \| "md" \| "lg"` | `"md"`  | 행 높이 및 텍스트 크기  |
| striped    | `boolean`              | `false` | 줄무늬(지브라) 스타일   |
| onRowClick | `(row: any) => void`   | -       | 행 클릭 콜백        |
| rowCount   | `number`               | -       | 고정 행 개수        |
| className  | `string`               | `""`    | 외부 wrapper 클래스 |

---

**Column 정의**
```ts
interface Column {
  key: string;
  header: string;
  width?: string;
  align?: "left" | "center" | "right";
  render?: (row: any) => ReactNode;
}
```
| 속성     | 설명                  |
| ------ | ------------------- |
| key    | row 데이터에서 읽을 key    |
| header | 헤더에 표시될 텍스트         |
| width  | 컬럼 너비 (`px`, `%` 등) |
| align  | 텍스트 정렬              |
| render | 셀 커스텀 렌더 함수         |

---

**Size**
| size | 행 높이 | 텍스트 크기    |
| ---- | ---- | --------- |
| sm   | 32px | text-xs   |
| md   | 40px | text-sm   |
| lg   | 48px | text-base |

---

**Behavior**
- `columns` 정의에 따라 Header / Body 자동 생성
- `render`가 있는 컬럼은 커스텀 셀 UI 렌더링
- `striped` 활성 시 홀수 행 배경색 적용
- `onRowClick` 전달 시 행 클릭 가능
- 데이터가 없을 경우 **“데이터가 없습니다.”** 메시지 표시
- `rowCount` 지정 시:
  - 데이터 개수보다 많으면 빈 행으로 높이 유지

---

**Notes**
- 내부적으로 `TableHeader`, `TableBody` 컴포넌트로 분리
- Header / Body에 동일한 `rowSizeClass` 적용으로 행 높이 일관성 유지
- wrapper에 `overflow-x-auto` 적용으로 가로 스크롤 대응

---

### Pagination
**개요**

목록 데이터를 페이지 단위로 탐색할 수 있는 Pagination 컴포넌트입니다.  
전체 페이지를 일정 개수(`visibleCount`) 단위로 묶어 표시하며, 이전/다음 그룹 이동을 지원합니다.

---

**Usage**

```tsx
import Pagination from "@/components/Pagination";
```
기본 사용
```tsx
const [page, setPage] = useState(1);

<Pagination
  page={page}
  total={123}
  pageSize={10}
  onChange={setPage}
/>;
```
한 번에 보여줄 페이지 개수 조절
```tsx
<Pagination
  page={page}
  total={200}
  visibleCount={7}
  onChange={setPage}
/>
```
버튼 크기 조절
```tsx
<Pagination size="sm" />
<Pagination size="md" />
```

---

**Props**
| 이름           | 타입                       | 기본값    | 설명                  |
| ------------ | ------------------------ | ------ | ------------------- |
| page         | `number`                 | -      | 현재 페이지 번호 (1-based) |
| total        | `number`                 | -      | 전체 아이템 개수           |
| pageSize     | `number`                 | `10`   | 페이지당 아이템 개수         |
| visibleCount | `number`                 | `5`    | 한 번에 표시할 페이지 버튼 수   |
| onChange     | `(page: number) => void` | -      | 페이지 변경 콜백           |
| size         | `"sm" \| "md"`           | `"md"` | 버튼 크기               |
| className    | `string`                 | `""`   | 외부 클래스              |

---

**Size**
| size | 버튼 높이 | 아이콘 크기 |
| ---- | ----- | ------ |
| sm   | 28px  | 14px   |
| md   | 32px  | 16px   |

---

**Behavior**
- `total`과 `pageSize`를 기준으로 전체 페이지 수 자동 계산
- 현재 페이지가 속한 그룹만 페이지 버튼으로 표시
  - 예: `1~5`, `6~10`, `11~15`
- ◀ / ▶ 버튼은 페이지 단위가 아닌 그룹 단위 이동
- 현재 페이지는 활성 스타일로 강조 표시
- 첫 그룹 / 마지막 그룹에서는 Prev / Next 비활성화

---

**Accessibility**
- `aria-label="Pagination"` 적용
- 현재 페이지 버튼에 `aria-current="page"` 설정
- 이전/다음 그룹 버튼에 명확한 aria-label 제공

**Notes**
- `total <= 0`인 경우 Pagination 렌더링되지 않음
- 내부적으로 현재 페이지를 항상 `1 ~ totalPages` 범위로 보정
- Table, List, Search 결과 페이지네이션에 바로 사용 가능

---

### 캘린더

**개요**

시작일(start)과 종료일(end)을 **하나의 컴포넌트에서 선택**할 수 있는 Range Datepicker 컴포넌트입니다.  
임시 선택(draft) → 확인/취소 구조를 사용하여, 사용자가 명시적으로 “확인”을 눌렀을 때만 값이 확정됩니다.

---

**Usage**

```tsx
import Calendar, { RangeValue } from "@/components/Calendar";
```
기본 사용
```tsx
const [range, setRange] = useState<RangeValue>({
  start: null,
  end: null,
});

<Calendar
  value={range}
  onChange={(v) => setRange(v)}
/>;
```
팝업 위치 변경
```tsx
<Calendar position="top" />
<Calendar position="bottom" />
<Calendar position="left" />
<Calendar position="right" />
```
크기 조절
```tsx
<Calendar size="sm" />
<Calendar size="md" />
<Calendar size="lg" />
```
아이콘 숨기기
```tsx
<Calendar showIcon={false} />
```

---

**Props**
| 이름        | 타입                                           | 기본값        | 설명            |
| --------- | -------------------------------------------- | ---------- | ------------- |
| value     | `{ start: Date \| null; end: Date \| null }` | -          | 선택된 날짜 범위     |
| onChange  | `(value: RangeValue) => void`                | -          | 날짜 범위 확정 콜백   |
| position  | `"top" \| "bottom" \| "left" \| "right"`     | `"bottom"` | 캘린더 팝업 위치     |
| size      | `"sm" \| "md" \| "lg"`                       | `"md"`     | Datepicker 크기 |
| showIcon  | `boolean`                                    | `true`     | 인풋 왼쪽 아이콘 표시  |
| className | `string`                                     | `""`       | 외부 래퍼 클래스     |

---

**Size**
| size | Input 높이 | 캘린더 너비 | 날짜 셀 높이 | 아이콘  |
| ---- | -------- | ------ | ------- | ---- |
| sm   | 32px     | 240px  | 28px    | 14px |
| md   | 40px     | 288px  | 32px    | 16px |
| lg   | 48px     | 320px  | 40px    | 20px |

---
**Behavior**
- 인풋 클릭 시 캘린더 팝업 열림
- 날짜 선택 흐름:
  - 첫 클릭 → 시작일(start)
  - 두 번째 클릭 → 종료일(end)
  - “확인” 클릭 시 `onChange(draft)` 호출
- “취소” 클릭 시:
  - `{ start: null, end: null }`으로 초기화
  - 팝업 닫힘
- 선택된 범위는 배경색으로 강조 표시
- 동일한 날짜(start === end)도 정상 처리

---

**Range Highlight 규칙**
- start === end
  → 단일 날짜 선택 (rounded-md)
- start만 선택됨
  → 시작 날짜만 강조
- start ~ end 사이
  → `bg-main/20`으로 범위 표시
- start / end
  → 좌·우 rounded 처리

---

**Notes**

- 내부적으로 `draft` 상태를 사용하여 확정 전 임시 선택 구현
- viewMonth / viewYear 상태로 월 이동 처리
- 날짜 비교는 `toDateString()` 기준
- Button 컴포넌트 재사용 (취소 / 확인)

---

### 기타
- **alert, toast**도 레포지토리에 포함되어 있습니다.
- `utils/format` 내부에 날짜(`date.ts`), 숫자(`number.ts`), 시간(`time.ts`)을 원하는 포맷으로 변환해주는 hook이 포함되어 있습니다.
- `tailwind.config.js`에 `main`, `sub1`, `sub2`에 대한 색상 지정이 되어있습니다. 

---

<br>

## 라이선스 (License)
본 가이드는 MIT 라이선스 하에 공개합니다

- 공유 복제, 배포, 포맷 변경, 전송, 전시, 공연, 방송할 수 있습니다.
- 변경 리믹스, 변형, 2차적 저작물 작성 및 영리목적의 이용이 가능합니다.
