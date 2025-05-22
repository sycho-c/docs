# 리액트 레이아웃 구조화 완벽 가이드

## 소개

이 문서는 React 애플리케이션에서 레이아웃을 효과적으로 구조화하는 방법에 대한 포괄적인 가이드입니다. 프론트엔드 개발 경험이 적은 백엔드 개발자도 이해할 수 있도록 기본 개념부터 시작하여 MyTalkPage.tsx 파일에서 사용된 고급 레이아웃 패턴까지 상세히 설명합니다.

레이아웃 구조화는 확장 가능하고 유지보수가 용이한 프론트엔드 애플리케이션을 개발하는 데 있어 핵심적인 요소입니다. 효과적인 레이아웃 구조는 다음과 같은 이점을 제공합니다:

- **코드 재사용성 증가**: 일관된 레이아웃 컴포넌트를 통해 중복 코드를 줄임
- **유지보수 용이성**: 명확한 구조로 코드 이해 및 수정이 쉬워짐
- **개발 효율성**: 정립된 패턴으로 새로운 기능 개발 속도 향상
- **사용자 경험 일관성**: 일관된 UI/UX 제공

이 가이드에서는 현재 사용 중인 MyTalkPage.tsx 코드를 분석하고, 이를 통해 효과적인 레이아웃 설계 방법론을 소개합니다.

## 목차

1. [프론트엔드 레이아웃 기초 개념](#프론트엔드-레이아웃-기초-개념)
2. [리액트 컴포넌트 구조의 이해](#리액트-컴포넌트-구조의-이해)
3. [복합 컴포넌트 패턴 심층 분석](#복합-컴포넌트-패턴-심층-분석)
4. [레이아웃 컴포넌트 계층 구조](#레이아웃-컴포넌트-계층-구조)
5. [컨텍스트 API를 활용한 상태 관리](#컨텍스트-API를-활용한-상태-관리)
6. [레이아웃 구조화 단계별 가이드](#레이아웃-구조화-단계별-가이드)
7. [오버레이 콘텐츠 관리 전략](#오버레이-콘텐츠-관리-전략)
8. [반응형 레이아웃 설계](#반응형-레이아웃-설계)
9. [레이아웃 성능 최적화](#레이아웃-성능-최적화)
10. [레이아웃 리팩토링 전략](#레이아웃-리팩토링-전략)
11. [확장성을 고려한 레이아웃 설계](#확장성을-고려한-레이아웃-설계)
12. [실제 사례 분석: MyTalkPage](#실제-사례-분석-mytalkpage)
13. [자주 발생하는 레이아웃 문제와 해결 방법](#자주-발생하는-레이아웃-문제와-해결-방법)
14. [결론 및 모범 사례](#결론-및-모범-사례)

---

## 프론트엔드 레이아웃 기초 개념

### 레이아웃이란?

프론트엔드 개발에서 '레이아웃'이란 웹 애플리케이션의 시각적 구조를 정의하는 방식을 의미합니다. 레이아웃은 화면에 표시되는 요소들의 배치, 크기, 위치 관계를 결정하며, 사용자 경험의 기초가 됩니다.

### 레이아웃의 주요 구성 요소

1. **컨테이너(Container)**: 다른 요소들을 포함하는 가장 기본적인 레이아웃 요소
2. **헤더(Header)**: 페이지 상단에 위치하며 주로 로고, 내비게이션, 검색창 등을 포함
3. **푸터(Footer)**: 페이지 하단에 위치하며 주로 저작권 정보, 연락처, 링크 등을 포함
4. **메인 콘텐츠(Main Content)**: 페이지의 주요 내용을 담는 영역
5. **사이드바(Sidebar)**: 주로 메인 콘텐츠 옆에 위치하며 부가 정보나 내비게이션 제공
6. **그리드(Grid)**: 콘텐츠를 행과 열로 구성하여 정렬된 배치 제공
7. **카드(Cards)**: 관련 정보를 그룹화하여 시각적으로 구분된 단위로 표시
8. **모달/오버레이(Modal/Overlay)**: 주 콘텐츠 위에 표시되는 팝업 요소

### HTML과 CSS를 사용한 기본적인 레이아웃 구성

기본적인 레이아웃은 HTML과 CSS를 사용하여 구성할 수 있습니다. 예시로 간단한 레이아웃 구성을 살펴보겠습니다:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }
    .container {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }
    header {
      background-color: #333;
      color: white;
      padding: 1rem;
    }
    main {
      display: flex;
      flex: 1;
    }
    .content {
      flex: 1;
      padding: 1rem;
    }
    .sidebar {
      width: 250px;
      background-color: #f0f0f0;
      padding: 1rem;
    }
    footer {
      background-color: #333;
      color: white;
      padding: 1rem;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>웹사이트 제목</h1>
    </header>
    <main>
      <div class="content">
        <h2>메인 콘텐츠</h2>
        <p>이곳에 주요 내용이 들어갑니다.</p>
      </div>
      <div class="sidebar">
        <h3>사이드바</h3>
        <ul>
          <li>링크 1</li>
          <li>링크 2</li>
          <li>링크 3</li>
        </ul>
      </div>
    </main>
    <footer>
      <p>© 2023 웹사이트. 모든 권리 보유.</p>
    </footer>
  </div>
</body>
</html>
```

### 현대적인 레이아웃 방식

현대적인 웹 개발에서는 더 복잡하고 동적인 레이아웃 구성을 위해 다양한 방식을 사용합니다:

1. **Flexbox**: 1차원 레이아웃 시스템으로, 행 또는 열 방향으로 항목을 유연하게 배치
2. **CSS Grid**: 2차원 레이아웃 시스템으로, 행과 열을 동시에 제어
3. **CSS 프레임워크**: Bootstrap, Tailwind CSS 등을 사용한 빠른 레이아웃 구성
4. **컴포넌트 기반 설계**: React, Vue 등의 프레임워크를 사용한 컴포넌트 기반 레이아웃

### 모바일 우선(Mobile First) 접근법

현대 웹 개발에서는 모바일 기기를 우선 고려하는 '모바일 우선' 접근법이 일반적입니다:

```css
/* 모바일 기본 스타일 */
.container {
  flex-direction: column;
}

/* 태블릿 이상 화면 */
@media (min-width: 768px) {
  .container {
    flex-direction: row;
  }
  
  .sidebar {
    width: 250px;
  }
}

/* 데스크톱 화면 */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;
  }
}
```

---

## 리액트 컴포넌트 구조의 이해

### 리액트 컴포넌트란?

React 컴포넌트는 UI를 구성하는 독립적이고 재사용 가능한 코드 조각입니다. 컴포넌트는 자체 상태와 로직을 가질 수 있으며, 다른 컴포넌트와 조합하여 복잡한 UI를 구성할 수 있습니다.

### 컴포넌트 유형

#### 함수형 컴포넌트(Functional Component)

현대 React 개발에서 권장되는 방식으로, 함수로 컴포넌트를 정의합니다:

```tsx
import React from 'react';

type ButtonProps = {
  text: string;
  onClick: () => void;
};

function Button({ text, onClick }: ButtonProps): JSX.Element {
  return (
    <button className="button" onClick={onClick}>
      {text}
    </button>
  );
}

export default Button;
```

#### 클래스형 컴포넌트(Class Component)

React 초기부터 사용된 방식으로, ES6 클래스를 사용하여 컴포넌트를 정의합니다:

```tsx
import React, { Component } from 'react';

type ButtonProps = {
  text: string;
  onClick: () => void;
};

class Button extends Component<ButtonProps> {
  render() {
    const { text, onClick } = this.props;
    return (
      <button className="button" onClick={onClick}>
        {text}
      </button>
    );
  }
}

export default Button;
```

### 컴포넌트 계층 구조

React 애플리케이션은 컴포넌트의 계층 구조로 이루어집니다:

```
App
├── Header
│   ├── Logo
│   └── Navigation
├── MainContent
│   ├── Sidebar
│   └── ContentArea
│       ├── ArticleList
│       │   └── ArticleItem
│       └── Pagination
└── Footer
```

이러한 계층 구조는 코드의 구조화와 재사용성을 높입니다.

### 프로퍼티(Props)와 상태(State)

#### Props

Props는 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달하는 방식입니다:

```tsx
// 부모 컴포넌트
function ParentComponent() {
  return <ChildComponent name="홍길동" age={30} />;
}

// 자식 컴포넌트
type ChildProps = {
  name: string;
  age: number;
};

function ChildComponent({ name, age }: ChildProps) {
  return (
    <div>
      <p>이름: {name}</p>
      <p>나이: {age}</p>
    </div>
  );
}
```

#### State

State는 컴포넌트 내부에서 관리되는 데이터로, 변경 시 컴포넌트가 리렌더링됩니다:

```tsx
import { useState } from 'react';

function Counter() {
  // count는 상태 변수, setCount는 상태를 업데이트하는 함수
  const [count, setCount] = useState<number>(0);

  return (
    <div>
      <p>카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
      <button onClick={() => setCount(count - 1)}>감소</button>
    </div>
  );
}
```

### 컴포넌트 생명주기(Lifecycle)

함수형 컴포넌트에서는 `useEffect` 훅을 사용하여 생명주기 이벤트를 처리합니다:

```tsx
import { useEffect, useState } from 'react';

function DataFetchingComponent() {
  const [data, setData] = useState<any>(null);
  const [loading, setLoading] = useState<boolean>(true);

  // 컴포넌트 마운트 시 실행
  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch('https://api.example.com/data');
        const result = await response.json();
        setData(result);
        setLoading(false);
      } catch (error) {
        console.error('데이터 가져오기 실패:', error);
        setLoading(false);
      }
    }

    fetchData();

    // 컴포넌트 언마운트 시 실행되는 클린업 함수
    return () => {
      console.log('컴포넌트가 언마운트됩니다');
    };
  }, []); // 빈 의존성 배열은 컴포넌트 마운트 시 한 번만 실행

  if (loading) return <div>로딩 중...</div>;
  if (!data) return <div>데이터가 없습니다</div>;

  return (
    <div>
      <h2>데이터 목록</h2>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}
```

### 타입스크립트와 리액트

TypeScript를 사용하면 컴포넌트의 프로퍼티와 상태에 타입을 지정할 수 있어 개발 시 오류를 줄이고 코드 품질을 향상시킬 수 있습니다:

```tsx
// 타입 정의
type UserProps = {
  id: number;
  name: string;
  email: string;
  isActive?: boolean; // 선택적 프로퍼티
};

// 타입을 사용한 컴포넌트
function UserProfile({ id, name, email, isActive = true }: UserProps): JSX.Element {
  return (
    <div className={`user-profile ${isActive ? 'active' : 'inactive'}`}>
      <h3>{name}</h3>
      <p>ID: {id}</p>
      <p>Email: {email}</p>
      <p>상태: {isActive ? '활성' : '비활성'}</p>
    </div>
  );
}
```

---

## 복합 컴포넌트 패턴 심층 분석

### 복합 컴포넌트 패턴이란?

복합 컴포넌트 패턴(Compound Component Pattern)은 여러 개의 관련 컴포넌트를 하나의 논리적 단위로 그룹화하는 방식입니다. 이 패턴은 복잡한 UI 컴포넌트를 모듈화하고 관련 컴포넌트 간의 관계를 명확히 하는 데 도움이 됩니다.

MyTalkPage.tsx 파일에서는 `TalkRoom`이라는 복합 컴포넌트를 사용하여 대화방 관련 UI 요소들을 논리적으로 그룹화하고 있습니다:

```tsx
<TalkRoom.Provider talkId={talkId}>
  <TalkRoom.Header rightMenus={headerMenus} />
  <TalkRoom.MenuDrawer open={activeDrawer} onOpen={...} onClose={...} />
  <TalkRoom.Content />
  <TalkRoom.TalkInfo />
  <TalkRoom.TalkParticipants />
  <TalkRoom.TalkAssigneeChange />
  <TalkRoom.TalkAdditionalInfoChange />
</TalkRoom.Provider>
```

### 복합 컴포넌트 패턴의 장점

1. **명확한 관계성**: 관련 컴포넌트들 간의 관계를 명확하게 표현
2. **사용성 향상**: 직관적인 API로 개발자가 쉽게 사용 가능
3. **코드 가독성**: 컴포넌트 간의 계층 구조를 명확하게 표현
4. **유연성**: 필요한 하위 컴포넌트만 선택적으로 사용 가능
5. **내부 상태 공유**: 컨텍스트를 통해 관련 컴포넌트 간 상태 공유 용이

### 복합 컴포넌트 패턴 구현 방법

#### 1. 네임스페이스 방식 구현

```tsx
// components/Menu/index.tsx
import MenuItem from './MenuItem';
import MenuHeader from './MenuHeader';
import MenuFooter from './MenuFooter';
import MenuDivider from './MenuDivider';

const Menu = (props) => {
  // 메인 Menu 컴포넌트 구현
  return <div className="menu">{props.children}</div>;
};

// 네임스페이스로 하위 컴포넌트 연결
Menu.Item = MenuItem;
Menu.Header = MenuHeader;
Menu.Footer = MenuFooter;
Menu.Divider = MenuDivider;

export default Menu;
```

사용 예시:

```tsx
import Menu from 'components/Menu';

function AppMenu() {
  return (
    <Menu>
      <Menu.Header>애플리케이션 메뉴</Menu.Header>
      <Menu.Item>홈</Menu.Item>
      <Menu.Item>프로필</Menu.Item>
      <Menu.Divider />
      <Menu.Item>설정</Menu.Item>
      <Menu.Footer>버전 1.0.0</Menu.Footer>
    </Menu>
  );
}
```

#### 2. 컨텍스트 API를 활용한 상태 공유

복합 컴포넌트는 컨텍스트 API를 활용하여 관련 컴포넌트 간의 상태를 공유할 수 있습니다:

```tsx
// components/Tabs/context.tsx
import React, { createContext, useState, useContext, ReactNode } from 'react';

type TabsContextType = {
  activeTab: string;
  setActiveTab: (id: string) => void;
};

const TabsContext = createContext<TabsContextType | undefined>(undefined);

// Provider 컴포넌트
export function TabsProvider({ children, defaultTab = '0' }: { children: ReactNode; defaultTab?: string }) {
  const [activeTab, setActiveTab] = useState(defaultTab);

  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      {children}
    </TabsContext.Provider>
  );
}

// 컨텍스트 사용을 위한 커스텀 훅
export function useTabsContext() {
  const context = useContext(TabsContext);
  if (context === undefined) {
    throw new Error('useTabsContext must be used within a TabsProvider');
  }
  return context;
}
```

```tsx
// components/Tabs/index.tsx
import { TabsProvider } from './context';
import TabList from './TabList';
import Tab from './Tab';
import TabPanel from './TabPanel';

function Tabs({ children, defaultTab }: { children: ReactNode; defaultTab?: string }) {
  return <TabsProvider defaultTab={defaultTab}>{children}</TabsProvider>;
}

Tabs.List = TabList;
Tabs.Tab = Tab;
Tabs.Panel = TabPanel;

export default Tabs;
```

```tsx
// components/Tabs/Tab.tsx
import { useTabsContext } from './context';

function Tab({ id, children }: { id: string; children: ReactNode }) {
  const { activeTab, setActiveTab } = useTabsContext();
  
  return (
    <button
      className={`tab ${activeTab === id ? 'active' : ''}`}
      onClick={() => setActiveTab(id)}
    >
      {children}
    </button>
  );
}

export default Tab;
```

사용 예시:

```tsx
import Tabs from 'components/Tabs';

function ProductInfo() {
  return (
    <Tabs defaultTab="details">
      <Tabs.List>
        <Tabs.Tab id="details">상세 정보</Tabs.Tab>
        <Tabs.Tab id="specs">제품 사양</Tabs.Tab>
        <Tabs.Tab id="reviews">리뷰</Tabs.Tab>
      </Tabs.List>
      
      <Tabs.Panel id="details">
        <p>이 제품은 최신 기술을 적용한 혁신적인 제품입니다.</p>
      </Tabs.Panel>
      <Tabs.Panel id="specs">
        <ul>
          <li>크기: 10 x 20 cm</li>
          <li>무게: 250g</li>
          <li>색상: 블랙</li>
        </ul>
      </Tabs.Panel>
      <Tabs.Panel id="reviews">
        <p>아직 리뷰가 없습니다.</p>
      </Tabs.Panel>
    </Tabs>
  );
}
```

#### 3. TypeScript를 활용한 복합 컴포넌트 타입 정의

TypeScript를 사용하면 복합 컴포넌트의 타입을 명확하게 정의할 수 있습니다:

```tsx
// components/Form/types.ts
import { ReactNode } from 'react';

export type FormProps = {
  onSubmit: (data: any) => void;
  children: ReactNode;
  initialValues?: Record<string, any>;
};

export type FormFieldProps = {
  name: string;
  label?: string;
  children: ReactNode;
  required?: boolean;
};

export type FormInputProps = {
  name: string;
  type?: 'text' | 'email' | 'password' | 'number';
  placeholder?: string;
  required?: boolean;
  value?: string;
  onChange?: (e: React.ChangeEvent<HTMLInputElement>) => void;
};

export type FormButtonProps = {
  type?: 'submit' | 'reset' | 'button';
  children: ReactNode;
  disabled?: boolean;
};
```

```tsx
// components/Form/index.tsx
import { FC } from 'react';
import { FormProps } from './types';
import FormField from './FormField';
import FormInput from './FormInput';
import FormButton from './FormButton';

const Form: FC<FormProps> & {
  Field: typeof FormField;
  Input: typeof FormInput;
  Button: typeof FormButton;
} = ({ onSubmit, children, initialValues = {} }) => {
  // 폼 구현...
  return (
    <form onSubmit={handleSubmit}>
      {children}
    </form>
  );
};

Form.Field = FormField;
Form.Input = FormInput;
Form.Button = FormButton;

export default Form;
```

### 실제 TalkRoom 복합 컴포넌트 구현 예시

MyTalkPage.tsx에서 사용된 TalkRoom 복합 컴포넌트의 실제 구현은 다음과 같을 수 있습니다:

```tsx
// components/mytalk/TalkRoom/index.tsx
import TalkRoomProvider from './context/TalkRoomProvider';
import Header from './sub/Header';
import Content from './sub/Content';
import MenuDrawer from './sub/MenuDrawer';
import TalkInfo from './sub/TalkInfo';
import TalkParticipants from './sub/TalkParticipants';
import TalkAssigneeChange from './sub/TalkAssigneeChange';
import TalkAdditionalInfoChange from './sub/TalkAdditionalInfoChange';

// 복합 컴포넌트로 구성
export const TalkRoom = {
  Provider: TalkRoomProvider,
  Header,
  Content,
  MenuDrawer,
  TalkInfo,
  TalkParticipants,
  TalkAssigneeChange,
  TalkAdditionalInfoChange,
};
```

```tsx
// components/mytalk/TalkRoom/context/TalkRoomProvider.tsx
import React, { createContext, useContext, useState, useEffect, ReactNode } from 'react';

// 컨텍스트 타입 정의
type TalkRoomContextType = {
  talkId: string;
  talkData: any | null;
  participants: any[];
  messages: any[];
  isLoading: boolean;
  error: string | null;
  sendMessage: (text: string) => void;
  // 기타 필요한 상태 및 함수들...
};

// 기본값으로 초기화된 컨텍스트 생성
const TalkRoomContext = createContext<TalkRoomContextType | undefined>(undefined);

// Provider 컴포넌트
function TalkRoomProvider({ 
  children, 
  talkId 
}: { 
  children: ReactNode; 
  talkId: string 
}): JSX.Element {
  const [talkData, setTalkData] = useState<any | null>(null);
  const [participants, setParticipants] = useState<any[]>([]);
  const [messages, setMessages] = useState<any[]>([]);
  const [isLoading, setIsLoading] = useState<boolean>(true);
  const [error, setError] = useState<string | null>(null);

  // 데이터 가져오기 로직
  useEffect(() => {
    async function fetchTalkData() {
      if (!talkId) return;
      
      setIsLoading(true);
      try {
        // API 호출 예시
        const response = await fetch(`/api/talks/${talkId}`);
        const data = await response.json();
        
        if (!response.ok) {
          throw new Error(data.message || '대화방 정보를 가져오는데 실패했습니다.');
        }
        
        setTalkData(data);
        setParticipants(data.participants || []);
        setMessages(data.messages || []);
        setError(null);
      } catch (err) {
        setError(err.message || '알 수 없는 오류가 발생했습니다.');
        console.error('Talk data fetch error:', err);
      } finally {
        setIsLoading(false);
      }
    }
    
    fetchTalkData();
  }, [talkId]);

  // 메시지 전송 함수
  const sendMessage = async (text: string) => {
    if (!text.trim() || !talkId) return;
    
    try {
      // API 호출 예시
      const response = await fetch(`/api/talks/${talkId}/messages`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ text }),
      });
      
      const newMessage = await response.json();
      
      if (!response.ok) {
        throw new Error(newMessage.message || '메시지 전송에 실패했습니다.');
      }
      
      // 새 메시지 추가
      setMessages(prevMessages => [...prevMessages, newMessage]);
    } catch (err) {
      console.error('Send message error:', err);
      // 오류 처리 로직
    }
  };

  // 컨텍스트 값 구성
  const value = {
    talkId,
    talkData,
    participants,
    messages,
    isLoading,
    error,
    sendMessage,
    // 기타 필요한 상태 및 함수들...
  };

  return (
    <TalkRoomContext.Provider value={value}>
      {children}
    </TalkRoomContext.Provider>
  );
}

// 커스텀 훅으로 컨텍스트 사용 간소화
export function useTalkRoom() {
  const context = useContext(TalkRoomContext);
  if (context === undefined) {
    throw new Error('useTalkRoom must be used within a TalkRoomProvider');
  }
  return context;
}

export default TalkRoomProvider;
```

```tsx
// components/mytalk/TalkRoom/sub/Header/index.tsx
import { useTalkRoom } from '../../context/TalkRoomProvider';
import TalkHeaderContainer from './container/TalkHeaderContainer';
import { TalkRoomHeaderSideMenuType } from './container/TalkHeaderContainer';

type HeaderProps = {
  rightMenus?: TalkRoomHeaderSideMenuType[];
};

function Header({ rightMenus = [] }: HeaderProps): JSX.Element {
  const { talkData, isLoading } = useTalkRoom();
  
  return (
    <TalkHeaderContainer
      title={talkData?.title || '대화방'}
      isLoading={isLoading}
      rightMenus={rightMenus}
    />
  );
}

export default Header;
```

이와 같은 방식으로 TalkRoom의 다른 하위 컴포넌트(Content, MenuDrawer 등)도 구현할 수 있습니다.

---

## 레이아웃 컴포넌트 계층 구조

### 계층적 레이아웃 구성의 중요성

레이아웃 컴포넌트를 계층적으로 구성하는 것은 다음과 같은 이점을 제공합니다:

1. **코드 재사용성**: 공통 레이아웃 구조를 여러 페이지에서 재사용
2. **일관성**: 애플리케이션 전체에 걸쳐 일관된 UI/UX 제공
3. **유지보수성**: 레이아웃 변경 시 중앙 집중식 수정 가능
4. **관심사 분리**: UI 구조와 페이지 콘텐츠 로직 분리

### PageLayout 컴포넌트 구조 분석

MyTalkPage.tsx에서 사용된 `PageLayout` 컴포넌트는 애플리케이션의 핵심 레이아웃 구조를 정의합니다:

```tsx
<PageLayout>
  <TalkRoom.Header rightMenus={headerMenus} />
  <TalkRoom.MenuDrawer
    open={activeDrawer}
    onOpen={...}
    onClose={...}
  />
  <PageLayout.MainContent>
    <TalkRoom.Content />
  </PageLayout.MainContent>
  <PageLayout.OverlayContent id={'talkInfo'}>
    <OverlayPageHeader title={t('button.talkInfo')} panelId={'talkInfo'} />
    <TalkRoom.TalkInfo />
  </PageLayout.OverlayContent>
  {/* 기타 오버레이 콘텐츠... */}
</PageLayout>
```

이 구조는 다음과 같은 계층으로 구성되어 있습니다:

1. **최상위 컨테이너** (`<PageLayout>`): 페이지 전체 구조를 감싸는 컨테이너
2. **헤더 영역** (`<TalkRoom.Header>`): 페이지 상단 헤더 영역
3. **메뉴 드로어** (`<TalkRoom.MenuDrawer>`): 사이드에서 나타나는 메뉴 패널
4. **메인 콘텐츠 영역** (`<PageLayout.MainContent>`): 페이지의 주요 콘텐츠를 담는 영역
5. **오버레이 콘텐츠 영역** (`<PageLayout.OverlayContent>`): 필요시 표시되는 오버레이 패널들

### PageLayout 컴포넌트 구현 예시

다음은 MyTalkPage.tsx에서 사용된 PageLayout 컴포넌트의 예상 구현입니다:

```tsx
// components/layout/PageLayout.tsx
import React, { ReactNode } from 'react';
import './PageLayout.scss'; // 스타일 가정

type PageLayoutProps = {
  children: ReactNode;
  className?: string;
};

function PageLayout({ children, className = '' }: PageLayoutProps): JSX.Element {
  return (
    <div className={`page-layout ${className}`}>
      {children}
    </div>
  );
}

// 메인 콘텐츠 영역 컴포넌트
type MainContentProps = {
  children: ReactNode;
  className?: string;
};

function MainContent({ children, className = '' }: MainContentProps): JSX.Element {
  return (
    <main className={`page-layout__main-content ${className}`}>
      {children}
    </main>
  );
}

// 오버레이 콘텐츠 영역 컴포넌트
type OverlayContentProps = {
  id: string;
  children: ReactNode;
  className?: string;
};

function OverlayContent({ id, children, className = '' }: OverlayContentProps): JSX.Element {
  return (
    <div 
      id={id} 
      className={`page-layout__overlay-content ${className}`}
      data-panel-id={id}
    >
      {children}
    </div>
  );
}

// Header 컴포넌트
type HeaderProps = {
  children: ReactNode;
  className?: string;
};

function Header({ children, className = '' }: HeaderProps): JSX.Element {
  return (
    <header className={`page-layout__header ${className}`}>
      {children}
    </header>
  );
}

// Footer 컴포넌트
type FooterProps = {
  children: ReactNode;
  className?: string;
};

function Footer({ children, className = '' }: FooterProps): JSX.Element {
  return (
    <footer className={`page-layout__footer ${className}`}>
      {children}
    </footer>
  );
}

// 서브 컴포넌트들을 PageLayout의 속성으로 할당
PageLayout.MainContent = MainContent;
PageLayout.OverlayContent = OverlayContent;
PageLayout.Header = Header;
PageLayout.Footer = Footer;

export default PageLayout;
```

### 스타일링 접근 방식

PageLayout 컴포넌트와 관련 서브 컴포넌트들의 스타일은 다음과 같은 방법으로 구현할 수 있습니다:

```scss
// components/layout/PageLayout.scss

// 기본 레이아웃 컨테이너
.page-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
  
  // 헤더
  &__header {
    position: sticky;
    top: 0;
    z-index: 100;
    background-color: #fff;
    border-bottom: 1px solid #e0e0e0;
  }
  
  // 메인 콘텐츠 영역
  &__main-content {
    flex: 1;
    padding: 1rem;
    overflow-y: auto;
    
    @media (min-width: 768px) {
      padding: 1.5rem;
    }
  }
  
  // 오버레이 콘텐츠 영역
  &__overlay-content {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #fff;
    z-index: 200;
    transform: translateX(100%);
    transition: transform 0.3s ease-in-out;
    
    &.active {
      transform: translateX(0);
    }
  }
  
  // 푸터
  &__footer {
    background-color: #f5f5f5;
    padding: 1rem;
    border-top: 1px solid #e0e0e0;
  }
}
```

### 레이아웃 컴포넌트 활용 패턴

레이아웃 컴포넌트를 효과적으로 활용하기 위한 몇 가지 패턴을 살펴보겠습니다:

#### 1. 페이지 템플릿 패턴

여러 페이지에서 공통으로 사용되는 레이아웃 구조를 템플릿으로 정의합니다:

```tsx
// templates/DefaultPageTemplate.tsx
import PageLayout from 'components/layout/PageLayout';
import Header from 'components/common/Header';
import Footer from 'components/common/Footer';

type DefaultPageTemplateProps = {
  children: ReactNode;
  title: string;
};

function DefaultPageTemplate({ children, title }: DefaultPageTemplateProps): JSX.Element {
  return (
    <PageLayout>
      <PageLayout.Header>
        <Header title={title} />
      </PageLayout.Header>
      
      <PageLayout.MainContent>
        {children}
      </PageLayout.MainContent>
      
      <PageLayout.Footer>
        <Footer />
      </PageLayout.Footer>
    </PageLayout>
  );
}

export default DefaultPageTemplate;
```

사용 예시:

```tsx
// pages/HomePage.tsx
import DefaultPageTemplate from 'templates/DefaultPageTemplate';
import HomeContent from 'components/home/HomeContent';

function HomePage(): JSX.Element {
  return (
    <DefaultPageTemplate title="홈">
      <HomeContent />
    </DefaultPageTemplate>
  );
}
```

#### 2. 조건부 레이아웃 렌더링

사용자 권한이나 상태에 따라 다른 레이아웃을 조건부로 렌더링합니다:

```tsx
// components/layout/ConditionalLayout.tsx
import { useAuth } from 'contexts/AuthContext';
import AdminLayout from './AdminLayout';
import UserLayout from './UserLayout';
import GuestLayout from './GuestLayout';

function ConditionalLayout({ children }: { children: ReactNode }): JSX.Element {
  const { user, isAuthenticated, isAdmin } = useAuth();
  
  if (isAdmin) {
    return <AdminLayout>{children}</AdminLayout>;
  }
  
  if (isAuthenticated) {
    return <UserLayout>{children}</UserLayout>;
  }
  
  return <GuestLayout>{children}</GuestLayout>;
}

export default ConditionalLayout;
```

#### 3. 중첩 레이아웃 패턴

페이지별 특수 요구사항을 위해 기본 레이아웃 내에 중첩된 레이아웃을 구현합니다:

```tsx
// pages/SettingsPage.tsx
import DefaultPageTemplate from 'templates/DefaultPageTemplate';
import SettingsSidebar from 'components/settings/SettingsSidebar';
import SettingsContent from 'components/settings/SettingsContent';

function SettingsPage(): JSX.Element {
  return (
    <DefaultPageTemplate title="설정">
      <div className="settings-layout">
        <div className="settings-layout__sidebar">
          <SettingsSidebar />
        </div>
        <div className="settings-layout__content">
          <SettingsContent />
        </div>
      </div>
    </DefaultPageTemplate>
  );
}
```

---

## 컨텍스트 API를 활용한 상태 관리

### React 컨텍스트 API 개요

React의 Context API는 컴포넌트 트리 전체에 데이터를 전달할 수 있는 방법을 제공합니다. 이는 여러 계층의 컴포넌트를 통해 props를 전달하는 "prop drilling" 문제를 해결합니다.

MyTalkPage.tsx에서는 `TalkRoom.Provider`를 통해 대화방 관련 상태와 로직을 하위 컴포넌트들에 전달하고 있습니다:

```tsx
<TalkRoom.Provider talkId={talkId}>
  {/* 여러 TalkRoom 컴포넌트들 */}
</TalkRoom.Provider>
```

### 컨텍스트 API 사용 방법

#### 1. 컨텍스트 생성

```tsx
// contexts/ThemeContext.tsx
import { createContext, useState, useContext, ReactNode } from 'react';

// 컨텍스트의 타입 정의
type ThemeContextType = {
  theme: 'light' | 'dark';
  toggleTheme: () => void;
};

// 컨텍스트 생성 및 기본값 설정
const ThemeContext = createContext<ThemeContextType | undefined>(undefined);

// Provider 컴포넌트
function ThemeProvider({ children }: { children: ReactNode }): JSX.Element {
  const [theme, setTheme] = useState<'light' | 'dark'>('light');
  
  const toggleTheme = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };
  
  // 컨텍스트 값 구성
  const value = {
    theme,
    toggleTheme,
  };
  
  return (
    <ThemeContext.Provider value={value}>
      {children}
    </ThemeContext.Provider>
  );
}

// 커스텀 훅으로 컨텍스트 사용 간소화
function useTheme() {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error('useTheme must be used within a ThemeProvider');
  }
  return context;
}

export { ThemeProvider, useTheme };
```

사용 예시:

```tsx
// App.tsx
import { ThemeProvider } from 'contexts/ThemeContext';

function App() {
  return (
    <ThemeProvider>
      <AppRoutes />
    </ThemeProvider>
  );
}
```

```tsx
// components/Header.tsx
import { useTheme } from 'contexts/ThemeContext';

function Header() {
  const { theme, toggleTheme } = useTheme();
  
  return (
    <header className={`header ${theme}`}>
      <h1>애플리케이션 제목</h1>
      <button onClick={toggleTheme}>
        {theme === 'light' ? '다크 모드로 전환' : '라이트 모드로 전환'}
      </button>
    </header>
  );
}
```

### 복합 컴포넌트와 컨텍스트 결합

복합 컴포넌트 패턴과 컨텍스트 API를 결합하면 강력한 레이아웃 상태 관리 방법을 구현할 수 있습니다:

```tsx
// components/mytalk/TalkRoom/context/TalkRoomContext.tsx
import { createContext, useContext, useState, useEffect, ReactNode } from 'react';

// 타입 정의 생략...

const TalkRoomContext = createContext<TalkRoomContextType | undefined>(undefined);

function TalkRoomProvider({ children, talkId }: { children: ReactNode; talkId: string }) {
  // 상태 및 로직 구현...
  
  return (
    <TalkRoomContext.Provider value={/* 컨텍스트 값 */}>
      {children}
    </TalkRoomContext.Provider>
  );
}

function useTalkRoom() {
  const context = useContext(TalkRoomContext);
  if (context === undefined) {
    throw new Error('useTalkRoom must be used within a TalkRoomProvider');
  }
  return context;
}

export { TalkRoomProvider, useTalkRoom };
```

```tsx
// components/mytalk/TalkRoom/index.tsx
import { TalkRoomProvider } from './context/TalkRoomContext';
import Header from './sub/Header';
import Content from './sub/Content';
// 기타 import...

export const TalkRoom = {
  Provider: TalkRoomProvider,
  Header,
  Content,
  // 기타 컴포넌트...
};
```

각 하위 컴포넌트는 `useTalkRoom` 훅을 통해 공유 상태에 접근할 수 있습니다:

```tsx
// components/mytalk/TalkRoom/sub/Content.tsx
import { useTalkRoom } from '../context/TalkRoomContext';

function Content() {
  const { messages, isLoading, error } = useTalkRoom();
  
  if (isLoading) return <div>로딩 중...</div>;
  if (error) return <div>에러: {error}</div>;
  if (messages.length === 0) return <div>메시지가 없습니다</div>;
  
  return (
    <div className="talk-content">
      {messages.map(message => (
        <MessageItem key={message.id} message={message} />
      ))}
    </div>
  );
}
```

### 여러 컨텍스트 조합하기

복잡한 애플리케이션에서는 여러 컨텍스트를 조합하여 사용할 수 있습니다:

```tsx
// App.tsx
import { ThemeProvider } from 'contexts/ThemeContext';
import { AuthProvider } from 'contexts/AuthContext';
import { NotificationProvider } from 'contexts/NotificationContext';

function App() {
  return (
    <ThemeProvider>
      <AuthProvider>
        <NotificationProvider>
          <AppRoutes />
        </NotificationProvider>
      </AuthProvider>
    </ThemeProvider>
  );
}
```

### 컨텍스트 최적화 고려사항

1. **불필요한 리렌더링 방지**: `React.memo`, `useMemo`, `useCallback`을 활용하여 최적화
2. **컨텍스트 분리**: 변경 빈도가 다른 상태는 별도의 컨텍스트로 분리
3. **상태 관리 라이브러리 고려**: 복잡한 상태의 경우 Redux, Zustand 등 고려

```tsx
// 최적화된 Provider 예시
function OptimizedProvider({ children }) {
  const [state1, setState1] = useState('state1');
  const [state2, setState2] = useState('state2');
  
  // 자주 변경되는 값
  const frequentlyChangingValue = useMemo(() => ({
    state1,
    setState1,
  }), [state1]);
  
  // 드물게 변경되는 값
  const rarelyChangingValue = useMemo(() => ({
    state2,
    setState2,
  }), [state2]);
  
  return (
    <FrequentContext.Provider value={frequentlyChangingValue}>
      <RareContext.Provider value={rarelyChangingValue}>
        {children}
      </RareContext.Provider>
    </FrequentContext.Provider>
  );
}
```

---

## 레이아웃 구조화 단계별 가이드

레이아웃을 효과적으로 구조화하기 위한 단계별 접근 방법을 살펴보겠습니다. 이 가이드는 새 프로젝트를 시작하거나 기존 프로젝트를 리팩토링할 때 유용합니다.

### 1. 레이아웃 요구사항 분석

레이아웃 설계의 첫 단계는 애플리케이션의 요구사항을 분석하는 것입니다:

- **페이지 유형 식별**: 애플리케이션에 필요한 페이지 유형 목록 작성 (예: 랜딩 페이지, 대시보드, 설정 페이지 등)
- **공통 UI 요소 식별**: 여러 페이지에서 반복되는 UI 요소 확인 (예: 헤더, 푸터, 사이드바 등)
- **페이지 내 섹션 식별**: 각 페이지 내에서 필요한 섹션 확인
- **내비게이션 구조 정의**: 페이지 간 이동 방식 및 사용자 플로우 정의
- **반응형 요구사항 정의**: 다양한 화면 크기에 대한 레이아웃 요구사항 정의

### 2. 핵심 레이아웃 컴포넌트 설계

분석한 요구사항을 바탕으로 핵심 레이아웃 컴포넌트를 설계합니다:

```tsx
// components/layout/BaseLayout.tsx
import React, { ReactNode } from 'react';

type BaseLayoutProps = {
  children: ReactNode;
};

function BaseLayout({ children }: BaseLayoutProps): JSX.Element {
  return <div className="base-layout">{children}</div>;
}

// 기본 레이아웃 하위 컴포넌트 정의
BaseLayout.Header = function Header({ children }: { children: ReactNode }): JSX.Element {
  return <header className="base-layout__header">{children}</header>;
};

BaseLayout.Footer = function Footer({ children }: { children: ReactNode }): JSX.Element {
  return <footer className="base-layout__footer">{children}</footer>;
};

BaseLayout.Sidebar = function Sidebar({ children }: { children: ReactNode }): JSX.Element {
  return <aside className="base-layout__sidebar">{children}</aside>;
};

BaseLayout.Content = function Content({ children }: { children: ReactNode }): JSX.Element {
  return <main className="base-layout__content">{children}</main>;
};

export default BaseLayout;
```

### 3. 페이지별 레이아웃 템플릿 구현

일반적인 페이지 유형에 대한 레이아웃 템플릿을 구현합니다:

```tsx
// templates/DashboardTemplate.tsx
import BaseLayout from 'components/layout/BaseLayout';
import DashboardHeader from 'components/dashboard/DashboardHeader';
import DashboardSidebar from 'components/dashboard/DashboardSidebar';
import DashboardFooter from 'components/dashboard/DashboardFooter';

type DashboardTemplateProps = {
  children: ReactNode;
  title: string;
};

function DashboardTemplate({ children, title }: DashboardTemplateProps): JSX.Element {
  return (
    <BaseLayout>
      <BaseLayout.Header>
        <DashboardHeader title={title} />
      </BaseLayout.Header>
      
      <BaseLayout.Content>
        {children}
      </BaseLayout.Content>
      
      <BaseLayout.Footer>
        <DashboardFooter />
      </BaseLayout.Footer>
    </BaseLayout>
  );
}

export default DashboardTemplate;
```

### 4. 기능별 복합 컴포넌트 구현

특정 기능에 관련된 UI 요소들을 복합 컴포넌트로 구현합니다:

```tsx
// components/dashboard/DashboardWidgets/index.tsx
import WidgetContainer from './WidgetContainer';
import StatWidget from './StatWidget';
import ChartWidget from './ChartWidget';
import ListWidget from './ListWidget';
import WidgetHeader from './WidgetHeader';

export const DashboardWidgets = {
  Container: WidgetContainer,
  Stat: StatWidget,
  Chart: ChartWidget,
  List: ListWidget,
  Header: WidgetHeader,
};
```

### 5. 상태 관리 전략 구현

레이아웃 상태 관리를 위한 컨텍스트를 구현합니다:

```tsx
// contexts/LayoutContext.tsx
import { createContext, useContext, useState, ReactNode } from 'react';

type LayoutContextType = {
  sidebarOpen: boolean;
  toggleSidebar: () => void;
  activeOverlay: string | null;
  showOverlay: (id: string) => void;
  hideOverlay: () => void;
};

const LayoutContext = createContext<LayoutContextType | undefined>(undefined);

function LayoutProvider({ children }: { children: ReactNode }): JSX.Element {
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [activeOverlay, setActiveOverlay] = useState<string | null>(null);
  
  const toggleSidebar = () => setSidebarOpen(prev => !prev);
  const showOverlay = (id: string) => setActiveOverlay(id);
  const hideOverlay = () => setActiveOverlay(null);
  
  const value = {
    sidebarOpen,
    toggleSidebar,
    activeOverlay,
    showOverlay,
    hideOverlay,
  };
  
  return (
    <LayoutContext.Provider value={value}>
      {children}
    </LayoutContext.Provider>
  );
}

function useLayout() {
  const context = useContext(LayoutContext);
  if (context === undefined) {
    throw new Error('useLayout must be used within a LayoutProvider');
  }
  return context;
}

export { LayoutProvider, useLayout };
```

### 6. 레이아웃 통합 및 라우팅

설계한 레이아웃 컴포넌트를 라우팅 시스템과 통합합니다:

```tsx
// routes/index.tsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import { LayoutProvider } from 'contexts/LayoutContext';
import HomePage from 'pages/HomePage';
import DashboardPage from 'pages/DashboardPage';
import SettingsPage from 'pages/SettingsPage';
import NotFoundPage from 'pages/NotFoundPage';

function AppRoutes() {
  return (
    <BrowserRouter>
      <LayoutProvider>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/dashboard" element={<DashboardPage />} />
          <Route path="/settings" element={<SettingsPage />} />
          <Route path="*" element={<NotFoundPage />} />
        </Routes>
      </LayoutProvider>
    </BrowserRouter>
  );
}

export default AppRoutes;
```

### 7. 페이지 구현

설계한 레이아웃 템플릿을 사용하여 개별 페이지를 구현합니다:

```tsx
// pages/DashboardPage.tsx
import DashboardTemplate from 'templates/DashboardTemplate';
import { DashboardWidgets } from 'components/dashboard/DashboardWidgets';

function DashboardPage(): JSX.Element {
  return (
    <DashboardTemplate title="대시보드">
      <h1>대시보드</h1>
      <div className="dashboard-grid">
        <DashboardWidgets.Container>
          <DashboardWidgets.Header title="통계" />
          <DashboardWidgets.Stat label="사용자 수" value="1,234" />
        </DashboardWidgets.Container>
        
        <DashboardWidgets.Container>
          <DashboardWidgets.Header title="활동" />
          <DashboardWidgets.Chart type="line" data={/* ... */} />
        </DashboardWidgets.Container>
        
        <DashboardWidgets.Container>
          <DashboardWidgets.Header title="최근 알림" />
          <DashboardWidgets.List items={/* ... */} />
        </DashboardWidgets.Container>
      </div>
    </DashboardTemplate>
  );
}

export default DashboardPage;
```

## 오버레이 콘텐츠 관리 전략

오버레이 콘텐츠는 메인 콘텐츠 위에 표시되는 UI 요소로, 모달, 드로어, 팝오버, 툴팁 등을 포함합니다. MyTalkPage.tsx에서는 여러 오버레이 콘텐츠를 효과적으로 관리하고 있습니다.

### 오버레이 콘텐츠의 종류

1. **모달(Modal)**: 사용자 작업을 중단시키고 응답을 요구하는 대화상자
2. **드로어(Drawer)**: 화면 가장자리에서 슬라이딩되어 나타나는 패널
3. **팝오버(Popover)**: 특정 요소를 클릭하면 나타나는 작은 오버레이
4. **툴팁(Tooltip)**: 요소에 마우스를 올리면 나타나는 짧은 설명
5. **패널(Panel)**: 전체 또는 부분 화면을 덮는 콘텐츠 영역

### MyTalkPage의 오버레이 콘텐츠 관리 패턴

MyTalkPage.tsx는 다양한 오버레이 콘텐츠를 `PageLayout.OverlayContent` 컴포넌트를 통해 일관되게 관리합니다:

```tsx
<PageLayout.OverlayContent id={'talkInfo'}>
  <OverlayPageHeader title={t('button.talkInfo')} panelId={'talkInfo'} />
  <TalkRoom.TalkInfo />
</PageLayout.OverlayContent>

<PageLayout.OverlayContent id={'talkParticipantsInfo'}>
  <OverlayPageHeader title={t('title.participantsInfo')} panelId={'talkParticipantsInfo'} />
  <TalkRoom.TalkParticipants />
</PageLayout.OverlayContent>
```

이 패턴의 주요 특징:

1. **고유 ID**: 각 오버레이 콘텐츠는 고유한 ID를 가짐
2. **일관된 구조**: 헤더와 콘텐츠 영역을 포함한 일관된 구조
3. **선언적 정의**: 페이지 컴포넌트 내에서 선언적으로 정의됨
4. **상태 관리 분리**: 표시 여부 상태는 별도로 관리됨

### 오버레이 관리를 위한 상태 관리 전략

오버레이 콘텐츠의 표시 여부를 효과적으로 관리하기 위한 상태 관리 전략을 살펴보겠습니다.

#### 1. 컨텍스트 기반 오버레이 관리

컨텍스트 API를 사용하여 중앙집중식으로 오버레이 상태를 관리하는 방법입니다:

```tsx
// contexts/OverlayContext.tsx
import { createContext, useContext, useState, ReactNode } from 'react';

type OverlayContextType = {
  activeOverlayId: string | null;
  showOverlay: (id: string) => void;
  hideOverlay: () => void;
  isOverlayActive: (id: string) => boolean;
};

const OverlayContext = createContext<OverlayContextType | undefined>(undefined);

function OverlayProvider({ children }: { children: ReactNode }): JSX.Element {
  const [activeOverlayId, setActiveOverlayId] = useState<string | null>(null);
  
  const showOverlay = (id: string) => setActiveOverlayId(id);
  const hideOverlay = () => setActiveOverlayId(null);
  const isOverlayActive = (id: string) => activeOverlayId === id;
  
  const value = {
    activeOverlayId,
    showOverlay,
    hideOverlay,
    isOverlayActive,
  };
  
  return (
    <OverlayContext.Provider value={value}>
      {children}
    </OverlayContext.Provider>
  );
}

function useOverlay() {
  const context = useContext(OverlayContext);
  if (context === undefined) {
    throw new Error('useOverlay must be used within an OverlayProvider');
  }
  return context;
}

export { OverlayProvider, useOverlay };
```

사용 예시:

```tsx
// components/layout/OverlayContent.tsx
import { useOverlay } from 'contexts/OverlayContext';

type OverlayContentProps = {
  id: string;
  children: ReactNode;
};

function OverlayContent({ id, children }: OverlayContentProps): JSX.Element {
  const { isOverlayActive } = useOverlay();
  const isActive = isOverlayActive(id);
  
  return (
    <div 
      className={`overlay-content ${isActive ? 'active' : ''}`}
      id={id}
      aria-hidden={!isActive}
    >
      {children}
    </div>
  );
}
```

#### 2. URL 기반 오버레이 관리

라우팅을 활용하여 오버레이 상태를 URL과 동기화하는 방법입니다:

```tsx
// routes/index.tsx
import { BrowserRouter, Routes, Route, useParams } from 'react-router-dom';
import MyTalkPage from 'pages/MyTalk/MyTalkPage';
import NotFoundPage from 'pages/NotFoundPage';

function AppRoutes() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/talks/:talkId" element={<MyTalkPage />} />
        <Route path="/talks/:talkId/:overlayId" element={<MyTalkPage />} />
        <Route path="*" element={<NotFoundPage />} />
      </Routes>
    </BrowserRouter>
  );
}

export default AppRoutes;
```

```tsx
// pages/MyTalk/MyTalkPage.tsx
import { useParams, useNavigate } from 'react-router-dom';

function MyTalkPage(): JSX.Element {
  const { talkId, overlayId } = useParams();
  const navigate = useNavigate();
  
  const showOverlay = (id: string) => {
    navigate(`/talks/${talkId}/${id}`);
  };
  
  const hideOverlay = () => {
    navigate(`/talks/${talkId}`);
  };
  
  const isOverlayActive = (id: string) => overlayId === id;
  
  // ...
}
```

#### 3. 복합 컴포넌트 기반 오버레이 관리

복합 컴포넌트 패턴을 활용하여 오버레이를 관리하는 방법입니다:

```tsx
// components/overlay/Overlay.tsx
import { createContext, useContext, useState, ReactNode } from 'react';

// 컨텍스트 정의...

const Overlay = ({ children }: { children: ReactNode }) => {
  const [activeId, setActiveId] = useState<string | null>(null);
  
  const contextValue = {
    activeId,
    setActiveId,
  };
  
  return (
    <OverlayContext.Provider value={contextValue}>
      {children}
    </OverlayContext.Provider>
  );
};

// 서브 컴포넌트 정의
Overlay.Trigger = function Trigger({ id, children }: { id: string; children: ReactNode }) {
  const { setActiveId } = useOverlayContext();
  
  return (
    <div onClick={() => setActiveId(id)}>
      {children}
    </div>
  );
};

Overlay.Content = function Content({ id, children }: { id: string; children: ReactNode }) {
  const { activeId, setActiveId } = useOverlayContext();
  const isActive = activeId === id;
  
  if (!isActive) return null;
  
  return (
    <div className="overlay-content active">
      <div className="overlay-backdrop" onClick={() => setActiveId(null)} />
      <div className="overlay-body">
        {children}
      </div>
    </div>
  );
};

export default Overlay;
```

사용 예시:

```tsx
<Overlay>
  <Overlay.Trigger id="userProfile">
    <button>프로필 보기</button>
  </Overlay.Trigger>
  
  <Overlay.Content id="userProfile">
    <UserProfileDetails />
  </Overlay.Content>
</Overlay>
```

### 오버레이 콘텐츠 접근성 고려

오버레이 콘텐츠 구현 시 접근성을 고려하는 것이 중요합니다:

1. **키보드 탐색**: 키보드만으로 오버레이를 조작할 수 있어야 함
2. **포커스 관리**: 오버레이 열기/닫기 시 포커스 이동 처리
3. **ARIA 속성**: `aria-hidden`, `aria-modal`, `role` 등 적절한 ARIA 속성 사용
4. **스크린 리더 지원**: 스크린 리더 사용자를 위한 적절한 텍스트 제공

```tsx
// 접근성을 고려한 모달 컴포넌트 예시
function AccessibleModal({ 
  isOpen, 
  onClose, 
  title, 
  children 
}: { 
  isOpen: boolean; 
  onClose: () => void; 
  title: string; 
  children: ReactNode;
}): JSX.Element | null {
  const modalRef = useRef<HTMLDivElement>(null);
  
  useEffect(() => {
    if (isOpen) {
      // 모달 열릴 때 포커스 이동
      modalRef.current?.focus();
      
      // ESC 키로 닫기 지원
      const handleKeyDown = (e: KeyboardEvent) => {
        if (e.key === 'Escape') onClose();
      };
      
      document.addEventListener('keydown', handleKeyDown);
      return () => document.removeEventListener('keydown', handleKeyDown);
    }
  }, [isOpen, onClose]);
  
  if (!isOpen) return null;
  
  return (
    <div 
      className="modal-overlay" 
      onClick={onClose}
      aria-hidden="true"
    >
      <div 
        ref={modalRef}
        className="modal-content" 
        onClick={e => e.stopPropagation()}
        role="dialog"
        aria-modal="true"
        aria-labelledby="modal-title"
        tabIndex={-1}
      >
        <h2 id="modal-title">{title}</h2>
        <div className="modal-body">{children}</div>
        <button 
          onClick={onClose}
          aria-label="닫기"
        >
          ×
        </button>
      </div>
    </div>
  );
}
```

### 오버레이 애니메이션 구현

사용자 경험을 향상시키기 위한 오버레이 애니메이션 구현 방법입니다:

```scss
// styles/overlay.scss
.overlay-content {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.3s, visibility 0.3s;
  
  &.active {
    visibility: visible;
    opacity: 1;
  }
  
  .overlay-body {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0.9);
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s;
    
    .active & {
      transform: translate(-50%, -50%) scale(1);
    }
  }
}

.drawer {
  position: fixed;
  top: 0;
  right: 0;
  height: 100%;
  width: 300px;
  background-color: white;
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.1);
  transform: translateX(100%);
  transition: transform 0.3s;
  z-index: 1000;
  
  &.active {
    transform: translateX(0);
  }
}
```

### 실제 프로젝트에서의 오버레이 관리 케이스 스터디

MyTalkPage.tsx의 오버레이 콘텐츠 관리 방식을 실제 프로젝트에 적용한 케이스 스터디입니다.

#### 케이스 1: 대시보드 페이지의 오버레이 관리

```tsx
// pages/DashboardPage.tsx
function DashboardPage(): JSX.Element {
  const [activeOverlay, setActiveOverlay] = useState<string | null>(null);
  
  return (
    <DashboardLayout>
      <DashboardLayout.Header>
        <h1>대시보드</h1>
        <button onClick={() => setActiveOverlay('settings')}>설정</button>
        <button onClick={() => setActiveOverlay('notifications')}>알림</button>
        <button onClick={() => setActiveOverlay('profile')}>프로필</button>
      </DashboardLayout.Header>
      
      <DashboardLayout.Content>
        {/* 대시보드 콘텐츠 */}
      </DashboardLayout.Content>
      
      <DashboardLayout.OverlayContent 
        id="settings"
        isActive={activeOverlay === 'settings'}
        onClose={() => setActiveOverlay(null)}
      >
        <SettingsPanel />
      </DashboardLayout.OverlayContent>
      
      <DashboardLayout.OverlayContent 
        id="notifications"
        isActive={activeOverlay === 'notifications'}
        onClose={() => setActiveOverlay(null)}
      >
        <NotificationsPanel />
      </DashboardLayout.OverlayContent>
      
      <DashboardLayout.OverlayContent 
        id="profile"
        isActive={activeOverlay === 'profile'}
        onClose={() => setActiveOverlay(null)}
      >
        <ProfilePanel />
      </DashboardLayout.OverlayContent>
    </DashboardLayout>
  );
}
```

#### 케이스 2: 전자상거래 사이트의 오버레이 관리

```tsx
// pages/ProductPage.tsx
function ProductPage(): JSX.Element {
  const { productId } = useParams();
  const [activeModal, setActiveModal] = useState<string | null>(null);
  
  return (
    <ShopLayout>
      <ShopLayout.Content>
        <ProductDetails 
          productId={productId} 
          onImageClick={() => setActiveModal('imageGallery')}
          onReviewsClick={() => setActiveModal('reviews')}
        />
      </ShopLayout.Content>
      
      <ShopLayout.Modal
        id="imageGallery"
        isOpen={activeModal === 'imageGallery'}
        onClose={() => setActiveModal(null)}
      >
        <ProductGallery productId={productId} />
      </ShopLayout.Modal>
      
      <ShopLayout.Modal
        id="reviews"
        isOpen={activeModal === 'reviews'}
        onClose={() => setActiveModal(null)}
      >
        <ProductReviews productId={productId} />
      </ShopLayout.Modal>
      
      <ShopLayout.Drawer
        id="cart"
        isOpen={activeModal === 'cart'}
        onClose={() => setActiveModal(null)}
      >
        <ShoppingCart />
      </ShopLayout.Drawer>
    </ShopLayout>
  );
}
```
