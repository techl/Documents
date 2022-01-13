# MFC Reverse Engineering

GetThisMessageMap을 찾고 하단에 AFX_MSGMAP_ENTRY 를 찾는다.

```
struct AFX_MSGMAP_ENTRY
{
        UINT nMessage;   // windows message
        UINT nCode;      // control code or WM_NOTIFY code
        UINT nID;        // control ID (or 0 for windows messages)
        UINT nLastID;    // used for entries specifying a range of control id's
        UINT_PTR nSig;       // signature type (action) or pointer to message #
        AFX_PMSG pfn;    // routine to call (or special value)
};
```

참고 : https://arisri.tistory.com/205