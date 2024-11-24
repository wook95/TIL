## persist

### Set, Map 객체 사용과 persist를 같이 사용하고 싶을 땐 ?

[공식문서](https://zustand.docs.pmnd.rs/integrations/persisting-store-data#createjsonstorage)

createJSONStorage의 두번째 인수의 options에 replacer와 reviver를 사용해서 직렬화와 역직렬화를 커스텀할 수 있다.

예시

```tsx
const createStore = (store: StateCreator<TodoCheckStore>) => {
  return persist(store, {
    name: "TODO::CHECKED",
    storage: createJSONStorage(() => localStorage, {
      // Serialize Set to Array
      replacer: (key, value) => {
        if (key === "checkedIds") {
          return Array.from(value as Set<string>);
        }
        return value;
      },
      // Deserialize Array to Set
      reviver: (key, value) => {
        if (key === "checkedIds") {
          return new Set(value as string[]);
        }
        return value;
      },
    }),
  });
};
```

### persist 옵션

- partialize: 상태의 일부만 저장하고 싶을 때 사용
- onRehydrateStorage: 수화 과정에서 추가 작업 가능
- version: 스토리지의 버전 관리 (기본값: 0)
- migrate: 버전 간 마이그레이션을 처리하는 함수
- merge: 저장된 상태와 현재 상태를 병합하는 방법을 커스터마이징 (기본값: shallow merge)
- skipHydration: 초기 hydration을 건너뛰고 수동으로 제어하고 싶을 때 사용

### persist API

스토어 외부에서도 persist 관련 작업을 할 수 있는 API 제공:

```typescript
// 옵션 가져오기
useBoundStore.persist.getOptions();

// 옵션 설정하기
useBoundStore.persist.setOptions({ name: "new-name" });

// 스토리지 초기화
useBoundStore.persist.clearStorage();

// 수동으로 rehydrate 실행
await useBoundStore.persist.rehydrate();

// hydration 상태 확인
useBoundStore.persist.hasHydrated();

// hydration 시작/종료 이벤트 리스너
useBoundStore.persist.onHydrate((state) => console.log("hydration 시작"));
useBoundStore.persist.onFinishHydration((state) =>
  console.log("hydration 완료")
);
```
