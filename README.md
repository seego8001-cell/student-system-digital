Edited
admin.tsx
src/routes/admin.tsx
    if (saved) {
      setCode(saved);
      login({ data: { code: saved } })
        .then(() => setAuthed(true))
        .catch(() => sessionStorage.removeItem("admin_code"));
        .then((r) => {
          if (r?.ok) setAuthed(true);
          else {
            sessionStorage.removeItem("admin_code");
            setCode("");
          }
        })
        .catch(() => {
          sessionStorage.removeItem("admin_code");
          setCode("");
        });
    }
  }, [login]);

  async function submit(e: React.FormEvent) {
    e.preventDefault();
    setErr("");
    const value = code.trim();
    try {
      await login({ data: { code } });
      sessionStorage.setItem("admin_code", code);
      const r = await login({ data: { code: value } });
      if (!r?.ok) {
        setErr("លេខកូដមិនត្រឹមត្រូវ");
        return;
      }
      setCode(value);
      sessionStorage.setItem("admin_code", value);
      setAuthed(true);
    } catch {
      setErr("លេខកូដមិនត្រឹមត្រូវ");
bunx tsgo --noEmit 2>&1 | tail -20; tail -20 /tmp/observability/build-errors.log 2>/dev/null