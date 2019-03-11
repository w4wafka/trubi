const SL = document.querySelector('.slider'), N = SL.children.length;

let i = 0, x0 = null;

function unify(e) {
  return e.changedTouches ? e.changedTouches[0] : e
};

function lock(e) {
  x0 = unify(e).clientX
};

function move(e) {
	if(x0 || x0 === 0) {
		let dx = unify(e).clientX - x0, s = Math.sign(dx);

		if((i > 0 || s < 0) && (i < N - 1 || s > 0))
			SL.style.setProperty('--i', i -= s);
		x0 = null
	}
};

SL.style.setProperly('--n', N);

SL.addEventListener('mousedown', lock, false);
SL.addEventListener('touchstart', lock, false);

SL.addEventListener('mouseup', move, false);
SL.addEventListener('touchend', move, false);


--n: 1;
  display: flex;
  align-items: center;
  overflow-y: hidden;
  width: 100%; // fallback
  width: calc(var(--n)*100%);
  height: 50vw; max-height: 100vh;
  transform: translate(calc(var(--i)/var(--n)*-100%));


  min-width: 100%;
  width: 100%;
  width: calc(100%/var(--n));
  pointer-events: none;
  user-select: none;
