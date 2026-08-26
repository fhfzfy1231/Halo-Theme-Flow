<script lang="ts">
  import { onMount } from "svelte";

  type HaloUser = {
    metadata?: { name?: string };
    spec?: {
      displayName?: string;
      avatar?: string;
    };
  };

  type CurrentUserResponse = {
    user?: HaloUser;
  };

  let user: HaloUser | null = null;
  let loading = true;
  let open = false;
  let accountMenu: HTMLDivElement;

  const displayName = () =>
    user?.spec?.displayName || user?.metadata?.name || "用户";

  async function loadCurrentUser() {
    try {
      const response = await fetch(
        "/apis/api.console.halo.run/v1alpha1/users/-",
        {
          credentials: "same-origin",
          headers: { Accept: "application/json" },
        },
      );

      if (!response.ok) {
        user = null;
        return;
      }

      const payload = (await response.json()) as CurrentUserResponse;
      const currentUser = payload.user;
      // Halo returns the disabled anonymousUser with HTTP 200 for visitors.
      user =
        currentUser?.metadata?.name &&
        currentUser.metadata.name !== "anonymousUser"
          ? currentUser
          : null;
    } catch {
      user = null;
    } finally {
      loading = false;
    }
  }

  function closeOnOutsideClick(event: MouseEvent) {
    if (open && accountMenu && !accountMenu.contains(event.target as Node)) {
      open = false;
    }
  }

  function closeOnEscape(event: KeyboardEvent) {
    if (event.key === "Escape") open = false;
  }

  onMount(() => {
    loadCurrentUser();
    document.addEventListener("click", closeOnOutsideClick);
    document.addEventListener("keydown", closeOnEscape);

    return () => {
      document.removeEventListener("click", closeOnOutsideClick);
      document.removeEventListener("keydown", closeOnEscape);
    };
  });
</script>

<div class="relative" bind:this={accountMenu}>
  {#if loading}
    <span
      class="btn-plain flex h-11 w-11 items-center justify-center rounded-lg opacity-60"
      aria-label="正在检查登录状态"
    >
      <span class="icon-[material-symbols--person-outline-rounded] text-[1.25rem]"></span>
    </span>
  {:else if !user}
    <a
      href="/login"
      class="btn-plain scale-animation flex h-11 items-center gap-1.5 rounded-lg px-3 font-bold active:scale-95"
      aria-label="登录"
    >
      <span class="icon-[material-symbols--login-rounded] text-[1.25rem]"></span>
      <span class="hidden xl:inline">登录</span>
    </a>
  {:else}
    <button
      type="button"
      class="btn-plain scale-animation flex h-11 items-center gap-1.5 rounded-lg px-2 active:scale-95"
      aria-label="账户菜单"
      aria-haspopup="menu"
      aria-expanded={open}
      on:click={() => (open = !open)}
    >
      {#if user.spec?.avatar}
        <img
          src={user.spec.avatar}
          alt=""
          class="h-7 w-7 rounded-full object-cover"
          referrerpolicy="no-referrer"
        />
      {:else}
        <span class="icon-[material-symbols--account-circle] text-[1.55rem]"></span>
      {/if}
      <span class="hidden max-w-24 truncate xl:inline">{displayName()}</span>
      <span
        class="icon-[material-symbols--expand-more-rounded] hidden text-sm transition-transform xl:inline"
        class:rotate-180={open}
      ></span>
    </button>

    {#if open}
      <div
        class="submenu-panel absolute right-0 top-full z-50 mt-3 w-44 rounded-(--radius-large) p-2"
        role="menu"
      >
        <div class="truncate px-3 py-2 text-sm font-bold text-(--primary)">
          {displayName()}
        </div>
        <div class="my-1 border-t border-black/10 dark:border-white/10"></div>
        <a
          href="/uc/profile"
          role="menuitem"
          class="flex items-center gap-2 rounded-lg px-3 py-2 transition hover:bg-(--btn-plain-bg-hover) dark:hover:bg-white/10"
        >
          <span class="icon-[material-symbols--person-outline-rounded] text-lg"></span>
          <span>个人中心</span>
        </a>
        <a
          href="/console"
          role="menuitem"
          class="flex items-center gap-2 rounded-lg px-3 py-2 transition hover:bg-(--btn-plain-bg-hover) dark:hover:bg-white/10"
        >
          <span class="icon-[material-symbols--dashboard-outline-rounded] text-lg"></span>
          <span>控制面板</span>
        </a>
        <a
          href="/logout"
          role="menuitem"
          class="flex items-center gap-2 rounded-lg px-3 py-2 text-red-500 transition hover:bg-red-500/10"
        >
          <span class="icon-[material-symbols--logout-rounded] text-lg"></span>
          <span>退出登录</span>
        </a>
      </div>
    {/if}
  {/if}
</div>
