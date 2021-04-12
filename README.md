CREATE TABLE public.albums
(
    id integer NOT NULL DEFAULT nextval('albums_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    years integer NOT NULL,
    id_singer integer,
    CONSTRAINT albums_pkey PRIMARY KEY (id),
    CONSTRAINT albums_id_singer_fkey FOREIGN KEY (id_singer)
        REFERENCES public.singer (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.albums
    OWNER to admin;

CREATE TABLE public.singer
(
    id integer NOT NULL DEFAULT nextval('singer_id_seq'::regclass),
    singer character varying(60) COLLATE pg_catalog."default" NOT NULL,
    alias character varying(60) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT singer_pkey PRIMARY KEY (id),
    CONSTRAINT singer_singer_key UNIQUE (singer)
)

TABLESPACE pg_default;

ALTER TABLE public.singer
    OWNER to admin;

CREATE TABLE public.track
(
    id integer NOT NULL DEFAULT nextval('track_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    duration integer NOT NULL,
    id_album integer,
    CONSTRAINT track_pkey PRIMARY KEY (id),
    CONSTRAINT track_id_album_fkey FOREIGN KEY (id_album)
        REFERENCES public.albums (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.track
    OWNER to admin;
