# MFC Reverse Engineering

GetThisMessageMap�� ã�� �ϴܿ� AFX_MSGMAP_ENTRY �� ã�´�.

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

���� : https://arisri.tistory.com/205