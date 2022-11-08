<template>
  <header id="header">
    <div className="header__left">
      <ul>
        <li>
          <a href="/about">About</a>
          <a href="/reference">Reference</a>
        </li>
      </ul>
    </div>
    <h1 className="header__center">
      <a href="/">API SITE</a>
    </h1>
    <div className="header__right">
      <ul>
        <li>
          <a href="/youtube">Youtube</a>
        </li>
        <li>
          <a href="/movie">Movie</a>
        </li>
        <li>
          <a href="/unsplash">Unsplash</a>
        </li>
      </ul>
    </div>
  </header>
</template>

<style lang="scss">
#header {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  border-bottom: 1px solid var(--bg-light-border);
  display: flex;
  align-items: center;
  background: var(--bg-light);
  z-index: 1000;

  a {
    color: var(--black);
    display: inline-block;
    position: relative;
    margin: 10px;

    &::before {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 1px;
      background: var(--black);
      transform: scale(0);
      transition: all 0.3s ease;
    }
    &:hover::before {
      transform: scale(1);
    }
  }

  li {
    display: inline-block;
  }

  .header__left {
    flex: 1 1 40%;
    font-family: var(--font-sub2);
  }
  .header__center {
    flex: 1 1 20%;
    text-align: center;
    font-size: 30px;
    font-family: var(--font-sub2);

    h1 a {
      padding: 10px 10px 12px 10px;
    }
  }
  .header__right {
    flex: 1 1 40%;
    text-align: right;
    font-family: var(--font-sub2);
  }
}
</style>
