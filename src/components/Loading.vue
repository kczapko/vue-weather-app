<template>
  <div class="loading">
    <svg
      xmlns:svg="http://www.w3.org/2000/svg"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      version="1.0"
      width="128px"
      height="128px"
      viewBox="0 0 128 128"
      xml:space="preserve"
    >
      <g>
        <path
          fill="#1e213a"
          fill-opacity="1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(30 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(60 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(90 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(120 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(150 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(180 64 64)"
        />
        <path
          fill="#e8e8eb"
          fill-opacity="0.1"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(210 64 64)"
        />
        <path
          fill="#d2d3d8"
          fill-opacity="0.2"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(240 64 64)"
        />
        <path
          fill="#a5a6b0"
          fill-opacity="0.4"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(270 64 64)"
        />
        <path
          fill="#787a89"
          fill-opacity="0.6"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(300 64 64)"
        />
        <path
          fill="#4b4d61"
          fill-opacity="0.8"
          d="M70.48 35.8l-6.16-6.24-6.16 6.26L64.32.88z"
          transform="rotate(330 64 64)"
        />
        <animateTransform
          attributeName="transform"
          type="rotate"
          values="0 64 64;30 64 64;60 64 64;90 64 64;120 64 64;150 64 64;180 64 64;210 64 64;240 64 64;270 64 64;300 64 64;330 64 64"
          calcMode="discrete"
          dur="1080ms"
          repeatCount="indefinite"
        ></animateTransform>
      </g>
    </svg>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.loading {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
